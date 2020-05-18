---
title: ag-grid
comments: true
categories:
  - Vue
tags:
  - ag-grid
  - Vue
abbrlink: ady7e5ef
date: 2020-02-09 10:02:06
---

## 0. 项目简介

> ag-Grid comes in two forms: ag-Grid Community (free for everyone, including production use) and ag-Grid Enterprise (you need a license to use).

简单来说就是`ag-Grid`有社区版和企业版两种，社区版面向全体人员，而企业版则只允许在开发环境使用。它可应用于`Angular`、`React`、`Vue`，由于我们项目使用到的是`Vue`，所以只从`Vue`的部分简单介绍。

## 1. 相关依赖

要想使用`ag-Grid`，相关的依赖自然是不可避免的，完整的依赖如下：

+ `@ag-grid-community/all-modules`：社区版的全部模块
+ `@ag-grid-community/vue`：提供 vue 支持
+ `@ag-grid-enterprise/all-modules`：企业版的全部模块
+ `@ag-grid-enterprise/core`：ag-Grid 核心逻辑
+ `vue-property-decorator`：作为 @ag-grid-community/vue 的依赖引入

## 2. 使用介绍

我节选了一段品牌商中使用到较全面的代码来介绍一下日常使用是什么样子：

```vue
<ag-grid-vue
  style="height: 632px;"
  class="ag-theme-balham"
  :columnDefs="columnsAg"
  :rowData="dataList"
  :suppressDragLeaveHidesColumns="true"
  :defaultColDef="defaultColDef"
  :enableCharts="true"
  :enableRangeSelection="true"
  :modules="modules"
  :getContextMenuItems="getContextMenuItems"
  :sideBar="{ toolPanels: ['columns','filters'] }"
  :localeText="agLangs"
  @gridReady="onReady" />
```

从上往下依次介绍：

+ `class`：支持三种主题:
  + ag-theme-balham
  + ag-theme-balham-dark
  + ag-theme-material

+ `columnDefs`：对比 iView 的 columns，具体内容下面会详细介绍
+ `rowData`：对比 iView 的 data
+ `suppressDragLeaveHidesColumns`：设置为 true 的时候可以防止将一列拖到表格外后隐藏
+ `defaultColDef`：默认行、列属性:
  + sortable:：可排序
  + resizable：可调整尺寸
  + filter：可过滤
  + autoHeight：自适应高度
  + // .......
+ `enableCharts`：开启极差图（与 enableRangeSelection 和 modules 同时使用）
+ `enableRangeSelection`：允许表格内范围选择
+ `modules`：加载模块
+ `getContextMenuItems`：定义表格内右键菜单项
+ `sideBar`：设置侧边功能栏，具体可看 [Side Bar](https://www.ag-grid.com/javascript-grid-side-bar/)，推荐使用对象设置:
  + toolPanels：这个设置也非常复杂，好在有幼儿版供我们使用—['columns', 'filters']，就不展开了
  + defaultToolPanel：默认展开的侧边栏
  + hiddenByDefault：是否隐藏侧边栏
  + position：侧边栏的位置（left、right）
+ `localeText`：语言包
+ `gridReady`：ag-Grid 初始完成事件，可以获得一个 params 对象:
  + type：事件名（"gridReady"）
  + api：ag-Grid API
  + columnApi：columns API，内部一个 columnController 对象，接着才是具体一些属性

基础的一些设置就是以上了，剩下的可以根据业务需求进行具体的查阅：

+ [ag-grid-vue 属性 VIP超全版](https://www.ag-grid.com/javascript-grid-properties/)
+ [ag-Grid API 头晕脑胀功能特别多版](https://www.ag-grid.com/javascript-grid-api/)
+ [ag-Grid Events SVIP一览无余版](https://www.ag-grid.com/javascript-grid-events/)
+ [ag-Grid Callbacks 不知道可以干些什么版](https://www.ag-grid.com/javascript-grid-callbacks/)

## 3. 表格行列

上面主要是一些基础设置，这个部分才是一个表格的灵魂。

下面抽取一段比较有代表性的代码：

```js
const columns = [
  {
    headerName: '商品名称',
    field: 'ProductVO.Name',
    width: 300,
    cellClass: 'special-cell',
    cellRenderer: 'agGroupCellRenderer',
    valueGetter: ({ data }) => data && data.ProductVO.Name,
    cellRendererParams: {
      innerRendererFramework: Vue.extend({
        template: `
          <div v-if="params.data" style="display: flex;align-items: center;height:100%;">
            <div style="width: 60px;text-align: center;">
              <img
                v-fancybox
                style="max-width: 60px;max-height: 60px;"
               :src="params.data.ProductVO.ImageUrl + '?x-oss-process=image/resize,h_60'">
            </div>
            <div style="margin: 0 0 0 10px;flex: 1;textAlign: left;">
              <p>{{ params.data.ProductVO.Name }}</p>
              <p>{{ params.data.ProductVO.BarCode }}</p>
            </div>
          </div>
        `,
      }),
    },
  },
  {
    headerName: '交易额',
    field: 'TotalPrice',
    width: 100,
    valueGetter: ({ data }) => data && Number((data.TotalPrice / 100).toFixed(2)),
    cellRenderer: (params) => {
      if (params.data) {
        return `￥${(params.data.TotalPrice / 100).toFixed(2)}`;
      }
      return priceCellRender(params);
    },
  },
  {
    headerName: '成交额',
    field: 'TotalPayPrice',
    width: 100,
    valueGetter: ({ data }) => data && Number((data.TotalPayPrice / 100).toFixed(2)),
    valueFormatter: (params) => {
      if (params.data) {
        return `￥${(params.data.TotalPayPrice / 100).toFixed(2)}`;
      }
      return priceCellRender(params);
    },
  },
  {
    headerName: '场地名称',
    field: 'TerminalVO.TerminalConfigVO.PlaceVO.Name',
    width: 130,
    valueGetter: ({ data }) => {
      let i = data && data.TerminalVO;
      if (isDef(i) && isDef(i = i.TerminalConfigVO) && isDef(i = i.PlaceVO)) {
        return i.Name || '';
      }
      return '';
    },
  },
  {
    headerName: '设备名称',
    field: 'TerminalVO.Name',
    width: 150,
  },
];
```

### 3.1 主要参数

| headerName | headerValueGetter |     field     |  width   |  hide  |  pinned  | sortable | ...  |
| :--------: | :---------------: | :-----------: | :------: | :----: | :------: | :------: | :--: |
|  列的名称  |    动态列名称     | data 中的字段 | 设置列宽 | 隐藏列 | 固定位置 |   排序   | 其他 |

### 3.2 表格渲染

表格渲染部分有很丶东西，比起`iView`的`render`来说，`ag-Grid`实在是`太太太太太太太`复杂了，从我上面的例子中也可见一斑，下面来从容易到复杂来介绍一下` ag-Grid`的渲染方式。

渲染方法主要有三种：

1. `valueGetter`：取代 field 字段，值是一个函数，形参有如下字段
+ 与 valueFormatter 相同的字段
  
+ getValue：函数，返回当前 value 的值
2. `valueFormatter`
+ 与 valueGetter 相同的字段
   + value：改变前的 value 值
3. `cellRenderer`
+ undefined / null：把 value 作为 string 渲染
   + String：grid 内置的组件名
   + Class：自己定义的组件
   + Function：一个返回 HTML 字符串或者 DOM 元素的函数
4. `cellRendererFramework`：这是 cellRenderer 的变体，可以直接引用组件类

==valueGetter、valueFormatter 相同字段==（~~这两货还接收类似 eval 里的写法，不推荐不介绍~~）


| data | node | column | colDef | api | columnApi | context |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| rowData 数据 | 行对象 | 列对象 | 行列配置项 | Grid API | 行列 API | 上下文 |

更多内容自行参考[官网](https://www.ag-grid.com/javascript-grid-cell-rendering/)，在下学不动了。

下图展示了`ag-Grid`如何来协作渲染的：

![valueGetterFlow](https://www.ag-grid.com/javascript-grid-value-getters/valueGetterFlow.svg)

经过我的一些简单摸(cai)索(keng)，建议渲染方式如下：

1. 直接输出：这种属于直接输出 data 里的值，通过`field`就可以了，例如上面的==设备名称==

2. 格式化后输出：常见于状态方面渲染，通过`valueGetter`使用，例如`Status`为0|1|2，渲染成==在线|离线|待投放==

3. 重组 value 与格式化输出：这种属于渲染内容与复制内容不同的情况，通过`valueGetter`和`vueFormatter`组合使用

4. 组件渲染：常见于==产品经理==，这种我又分为了两种情况:

   + 不需要分组：可直接通过`cellRendererFramework`渲染组件，例如一些操作类的 button、input、select 等

   + 需要分组，例如上面的==商品名称==

     ```js
     const columns = [
       {
         valueGetter: ({ data }) => data && data.XXX
         cellRenderer: 'agGroupCellRenderer',
         cellRendererParams: {
           innerRendererFramework: Vue.exntend(),
         },
       }
     ];
     ```

如果大家还有其他的发现，欢迎探讨来《深入浅出 ag-Grid》。