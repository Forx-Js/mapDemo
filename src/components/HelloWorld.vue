<template>
  <div class="hello">
    {{msg}}
    <div class="mapBox">
      <!--     zoom 范围      center 中心点     plugin 插件     class class名 -->
      <el-amap vid="MapDiv" :zoom="zoom" :center="center" :plugin="plugin" class="immap">
        <!-- 信息窗 -->
         <!-- position坐标   content内容  visible隐藏   events事件  -->
        <el-amap-info-window  :position="mywindow.position" :content="mywindow.content" :visible="mywindow.visible" :events="mywindow.events"></el-amap-info-window>
        <el-amap-marker :position="marker.position" :events="marker.events" :visible="marker.visible" :draggable="marker.draggable"></el-amap-marker>
        <el-amap-circle :center="circle.center" :radius="circle.radius" :fillOpacity="circle.fillOpacity" :events="circle.events" :strokeColor="circle.strokeColor" :strokeStyle="circle.strokeStyle" :fillColor="circle.fillColor"></el-amap-circle>
      </el-amap>
    </div>
   
  </div>
</template>

<script>
// 高德地图ui
// import VueAMap from "vue-amap";
// let amapManager = new VueAMap.AMapManager();
export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      zoom: 12,
      center: [117.954979, 34.950299],
      circle: {
        clickable: true,
        center: [121.5273285, 31.21515044],
        radius: 200,
        fillOpacity: 0.3,
        strokeStyle: "dashed",
        fillColor: "#FFFF00",
        strokeColor: "#00BFFF"
      },
      marker: {
        position: [121.5273285, 31.21515044],
        events: {
          click: () => {
            if (this.mywindow.visible === true) {
              this.mywindow.visible = false;
            } else {
              this.mywindow.visible = true;
            }
          },
          dragend: e => {
            this.markers[0].position = [e.lnglat.lng, e.lnglat.lat];
          }
        },
        visible: true,
        draggable: false
      },
      mywindow: {
        position: [121.5273285, 31.21515044],
        content:'我是窗体内容',
        visible: true,
        events: {
          close() {
            console.log(this);
          }
        }
      },
      plugin: {
        pName: "Scale",
        events: {
          init(instance) {
            console.log(instance);
          }
        }
      }
      // 高德地图ui
      // amapManager,
      // events: {
      // init(map) {
      //   // 点
      //   AMapUI.loadUI(['overlay/SimpleMarker'], SimpleMarker => {
      //     const marker = new SimpleMarker({
      //       iconLabel: "家",
      //       iconStyle: "red",
      //       iconTheme: 'default',
      //       map: map,
      //       position: map.getCenter()
      //     });
      //   });
      // }
      // }
    };
  }
};
</script>

<style scoped>
.mapBox {
  height: 500px;
}
</style>
