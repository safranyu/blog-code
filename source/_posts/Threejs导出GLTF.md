---
title: Threejs导出GLTF
comments: true
categories:
  - ThreeJs
tags:
  - ThreeJs
abbrlink: f781f6cc
date: 2020-12-15 15:08:30
---


> 需要在文件里引入`GLTFExporter.js`

```javascript
function save(blob, filename) {
    var link = document.createElement('a');
    link.style.display = 'none';
    link.href = URL.createObjectURL(blob);
    link.download = filename || 'data.json';
    link.click();
}
function saveString(text, filename) {
    save(new Blob([text], { type: 'text/plain' }), filename);
}
function OnExportGLTF() {
    var exporter = new THREE.GLTFExporter();
    exporter.parse(scene3D, (result)=>{
        saveString(JSON.stringify(result), `demo.gltf`)
    });
}
```

报错:`geometry.getAttribute is not a function`查看元素确实没有`getAttribute`方法，因此手动添加该方法解决报错

![](http://img.cdn.vmccc.cn/20201215145546.jpg)

```
// 在报错地方前面添加即可
if (typeof(geometry)=="object") {
	geometry.getAttribute = function (name) {
		return geometry[name];
	}
	geometry.addAttribute = function (name, val) {
		geometry[name] = val;
	}
}

```