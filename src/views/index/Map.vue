<script setup lang="ts">
import { ref, onMounted, defineEmits, watch } from "vue";
import { Scene, PointLayer } from "@antv/l7";
import { GaodeMap, Mapbox } from "@antv/l7-maps";
import points_data from "@/assets/points_data.json";
import WeatherInfoCard from "@/components/WeatherInfoCard.vue";

const emit = defineEmits(["update"]);

const selectedPoint = ref<{ lat: number; lng: number }>();
watch(selectedPoint, () => {
  emit("update", selectedPoint.value);
});

const initMap = () => {
  const scene = new Scene({
    id: "map",
    map: new GaodeMap({
      style: "blank",
      center: [107.054293, 35.246265],
      zoom: 4.056,
      // token: "36e7fbf6b069ab4834feb88a40bc562a",
      token: "4b8d96b56bed29b2df4a7713e3e1421e",
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
    .size(8)
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
  <div class="map-page">
    <div id="map" ></div>
  </div>
</template>

<style scoped lang="scss">
#map {
  width: 800px;
  height: 600px;
  position: relative;
}
</style>
