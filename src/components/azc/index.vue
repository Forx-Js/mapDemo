<template>
    <div class="amap-page-container">
      
    </div>
  </template>

  <style>
.mapbox {
  height: 500px;
}
.amap-demo {
  height: 300px;
}
</style>

  <script>
// NPM 方式
import VueAMap from "vue-amap";
let amapManager = new VueAMap.AMapManager();

export default {
  data() {
    return {
      // amapui
      amapManager,
      zoom: 13,
      centerCity: null,
      searchOption:{
        city:'济南',
        citylimit:true
      },
      center: [118.040504, 35.013608],
      events: {
        // 事件
        // 加载完成
        init: o => {
          // 中心经纬度
          // console.log(o.getCenter())
          // 地图对象  0 == this.$refs.map.$$getInstance().getCenter()
          // console.log(this.$refs.map.$$getInstance().getCenter())
          // 获取城市信息
          // o.getCity(result => {
          //   console.log(result);
          // });
        },
        // 移动事件
        moveend: () => {
          this.getcity(this.dd);
        },
        // 缩放事件 附带移动事件
        zoomchange: () => {
          console.log("进行缩放了");
        },
        // 点击地图
        click: e => {
          console.log(e);
        }
      },
      // 插件
      plugin: [
      // 控制器         
        "ToolBar",
        {
          //  卫星/地图+缩放栏
          pName: "MapType",
          defaultType: 0,
          events: {
            // 加载成功事件
            init(o) {
              // console.log(o);
            }
          }
        }
      ]
    };
  },

  methods: {
    getMap() {
      // amap vue component
      // 地图列表
      console.log(amapManager._componentMap.amapDemo);
      console.log(amapManager._map);
    },
    // 获取城市
    getcity() {
      // 异步函数
      this.$refs.map.$$getInstance().getCity(result => {
        this.centerCity = result;
      });
    },
    onSearchResult (j){
      // 搜索结果
      console.log(j);
    }
  },
  computed: {}
};
</script>