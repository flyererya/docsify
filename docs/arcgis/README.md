## 在vue中使用arcgis 

1. npm install --save esri-loader
2. 新建WebMap组件

```javascript
<template>
  <div></div>
</template>

<script>
import { loadModules } from 'esri-loader';

export default {
  name: 'web-map',
  mounted() {
    // lazy load the required ArcGIS API for JavaScript modules and CSS
    loadModules(['esri/Map', 'esri/views/MapView'], { css: true })
    .then(([ArcGISMap, MapView]) => {
      const map = new ArcGISMap({
        basemap: 'topo-vector'
      });

      this.view = new MapView({
        container: this.$el,
        map: map,
        center: [-118, 34],
        zoom: 8
      });
    });
  },
  beforeDestroy() {
    if (this.view) {
      // destroy the map view
      this.view.container = null;
    }
  }
};

</script>

<style scoped>
div {
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100%;
}
</style>
```
> 需要注意的是，这样是默认使用的4.x的arcgis


<br>
<br>
<br>
<br>

## 指定arcgis 版本
1. 在App.vue中引入css

```javascript
/* @import url('https://js.arcgis.com/3.32/esri/css/esri.css'); */
@import url('/3.13/3.13/esri/css/esri.css'); //写你自己本地部署的
```
2. 在WebMap.vue组件中配置

```javascript
const options = {
    // url: 'https://js.arcgis.com/3.32/'
    url:'/3.13/3.13/init.js' //写你自己本地部署的
}
```
3. 在mounted方法中

```javascript
mounted() {
        // lazy load the required ArcGIS API for JavaScript modules and CSS
        loadModules(['esri/map'],options).then(([Map]) => {
            var map = new Map('map', {
                basemap: 'dark-gray',
                center: [-111.879655861, 40.571338776] // long, lat
            })
        })
    },
```
> 注意注意！！！！！！！<br>
在3.x版本中模块的引入'esri/map' 里map是小写<br>
在4.x版本中是'esri/Map' 这里找了整整2个小时的bug  太坑了