<script setup lang="ts">
import { ref, onMounted, defineEmits, watch } from "vue";
import { Scene, PointLayer } from "@antv/l7";
import { GaodeMap } from "@antv/l7-maps";
import points_data from "@/assets/points_data.json";
import WeatherInfoCard from "@/src/views/index/Map.vue";
import BorderBox13 from "@/components/datav/border-box-13";

const emit = defineEmits(["update"]);

const selectedPoint = ref<{ lat: number; lng: number }>();
watch(selectedPoint, () => {
  emit("update", selectedPoint.value);
});

const initMap = () => {
  const scene = new Scene({
    id: "map",
    map: new GaodeMap({
      mapStyle: 'amap://styles/darkblue',
      center: [107.054293, 35.246265],
      zoom: 4.056,
      token: "36e7fbf6b069ab4834feb88a40bc562a",
      // token: "4b8d96b56bed29b2df4a7713e3e1421e",
      doubleClickZoom: false,
    }),
  });

  const pointLayer = new PointLayer()
    .source(points_data, {
      parser: {
        type: "json",
        x: "lng",
        y: "lat",
      },
    })
    .shape("circle")
    .size(5)
    .active(true)
    .color("red")
    .style({
      opacity: 0.5,
    });

  pointLayer.on("dblclick", (e) => {
    console.log('用户点击');
    const { lng, lat } = e.lngLat;
    selectedPoint.value = { lng, lat };
  });
  scene.addLayer(pointLayer);
};

onMounted(() => {
  console.log('地图初始化');
  initMap();
});
</script>

<template>
  <div class="maptitle">
      <div class="zuo"></div>
      <span class="titletext">监测站分布图</span>
      <div class="you"></div>
  </div>
  <div class="map-page">
    <BorderBox13>
      <div class="map-wrapper">
        <div id="map" ></div>
      </div>
    </BorderBox13>
  </div>
</template>

<style scoped lang="scss">
//控制画布大小
#map {
  width: 96%;
  height: 550px;
  position: relative;
}

.maptitle {
  height: 60px;
  display: flex;
  justify-content: center;
  padding-top: 10px;
  box-sizing: border-box;

  .titletext {
    font-size: 28px;
    font-weight: 900;
    letter-spacing: 6px;
    background: linear-gradient(92deg, #0072ff 0%, #00eaff 48.8525390625%, #01aaff 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    margin: 0 10px;
  }

  .zuo,
  .you {
    background-size: 100% 100%;
    width: 29px;
    height: 20px;
    margin-top: 8px;
  }

  .zuo {
    background: url("@/assets/img/xiezuo.png") no-repeat;
  }

  .you {
    background: url("@/assets/img/xieyou.png") no-repeat;
  }
}

//控制画布大小？
.map-page {
  height: 580px;
  width: 100%;
  box-sizing: border-box;
  position: relative;

  //控制画布左右位置
  .map-wrapper {
    padding: 17px 0 10px 25px;
  }
}
</style>
