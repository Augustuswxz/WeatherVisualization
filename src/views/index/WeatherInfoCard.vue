<script setup lang="ts">
import { ElMessage } from "element-plus";
import { column } from "element-plus/es/components/table-v2/src/common";
import { defineProps, watch, ref } from "vue";

interface WeatherInfoProps {
  pointData:
    | {
        lat: number;
        lng: number;
      }
    | undefined;
  date: string | undefined;
}
const props = defineProps<WeatherInfoProps>();
const DialogShow = ref(false);
const Record = ref<{
  WeatherStationCode : number;
  Date : string;
  Latitude : number;
  Longtitude : number;
  HeightOfMeteorologicalStation : number;
  NameOfMeteorologicalStation : string;
  AverageTemperature : number;
  AttributesOfAverageTemperature : number;
  AverageDewPoint : number;
  AttributesOfAverageDewPoint : number;
  AverageSeaLevelPressure : number;
  AttributesOfAverageSeaLevelPressure : number;
  AverageObservatoryPressure : number;
  AttributesOfAverageObservatoryPressure : number;
  AverageVisibility : number;
  AttributesOfAverageVisibility : number;
  AverageWindSpeed : number;
  AttributesOfAverageWindSpeed : number;
  MaximumSustainedWindSpeed : number;
  AttributesOfMaximumSustainedWindSpeed : number;
  HighestTemperature : number;
  AttributesOfHighestTemperature : number;
  LowestTemperature : number;
  AttributesOfLowestTemperature : number;
  Precipitation : number;
  AttributesOfPrecipitation : string;
  DepthOfSnow : number;
  Indicator : number;
}| undefined>(undefined);

Record.value = {
  WeatherStationCode : 1001099999,
  Date : "2022/1/1",
  Latitude : 70.9333333,
  Longtitude : -8.6666667,
  HeightOfMeteorologicalStation : 9,
  NameOfMeteorologicalStation : "JAN MAYEN NOR NAVY, NO",
  AverageTemperature : 12.1,
  AttributesOfAverageTemperature : 19,
  AverageDewPoint : 3.8,
  AttributesOfAverageDewPoint : 19,
  AverageSeaLevelPressure : 1010.2,
  AttributesOfAverageSeaLevelPressure : 19,
  AverageObservatoryPressure : 9,
  AttributesOfAverageObservatoryPressure : 19,
  AverageVisibility : 9.9,
  AttributesOfAverageVisibility : 4,
  AverageWindSpeed : 16.6,
  AttributesOfAverageWindSpeed : 19,
  MaximumSustainedWindSpeed : 27,
  AttributesOfMaximumSustainedWindSpeed : 35.5,
  HighestTemperature : 18,
  AttributesOfHighestTemperature : null,
  LowestTemperature : 9,
  AttributesOfLowestTemperature : null,
  Precipitation : 0.01,
  AttributesOfPrecipitation : "E",
  DepthOfSnow : 999.9,
  Indicator : 1000,
};

watch(
  () => props.pointData,
  (newVal) => {
    if (newVal) {
      // 当 pointData 有值时，显示弹窗
      DialogShow.value = true;
      console.log("用户点击散点",newVal);
    }
  }
);

// const Record = ref<{ [key: string]: any } | null>(null);
// watch(
//   () => [props.pointData, props.date],
//   async (newval) => {
//     const [pointData, date] = newval;
//     if(pointData & date){
//       try {
//         const response = await axios.get("url",{
//           params: {
//             lat : pointData.lat,
//             lng : pointData.lng,
//             date : date,
//           }
//         });
//         Record.value = response.data;
//         DialogShow.value = true;
//       } catch(error) {
//         ElMessage.error("获取气象记录失败，请稍后。");
//         DialogShow.value = false;
//       }
//     }
//   },
//   {immediate: true}
// );
</script>

<template>
  <div>
    <el-dialog 
      v-model="DialogShow" 
      title="气象信息" 
      width="80%" 
      draggable 
      :modal="false"
    >
      <el-descriptions 
				border
        size="large"
        :column="4"
			>
        <el-descriptions-item label="气象站代码">{{ Record?.WeatherStationCode }}</el-descriptions-item>
        <el-descriptions-item label="日期">{{Record?.Date}}</el-descriptions-item>
        <el-descriptions-item label="纬度">{{Record?.Latitude}}</el-descriptions-item>
        <el-descriptions-item label="经度">{{Record?.Longtitude}}</el-descriptions-item>
        <el-descriptions-item label="气象站高程">{{Record?.HeightOfMeteorologicalStation}}</el-descriptions-item>
        <el-descriptions-item label="气象站名称">{{Record?.NameOfMeteorologicalStation}}</el-descriptions-item>
        <el-descriptions-item label="平均气温">{{ Record?.AverageTemperature }}</el-descriptions-item>
        <el-descriptions-item label="平均气温属性">{{ Record?.AttributesOfAverageTemperature }}</el-descriptions-item>
        <el-descriptions-item label="平均露点">{{ Record?.AverageDewPoint }}</el-descriptions-item>
        <el-descriptions-item label="平均露点属性">{{ Record?.AttributesOfAverageDewPoint }}</el-descriptions-item>
        <el-descriptions-item label="平均海平面压强">{{ Record?.AverageSeaLevelPressure }}</el-descriptions-item>
        <el-descriptions-item label="平均海平面压强属性">{{ Record?.AttributesOfAverageSeaLevelPressure }}</el-descriptions-item>
        <el-descriptions-item label="平均观测站压强">{{ Record?.AverageObservatoryPressure }}</el-descriptions-item>
        <el-descriptions-item label="平均观测站压强属性">{{ Record?.AttributesOfAverageObservatoryPressure }}</el-descriptions-item>
        <el-descriptions-item label="平均能见度">{{ Record?.AverageVisibility }}</el-descriptions-item>
        <el-descriptions-item label="平均能见度属性">{{ Record?.AttributesOfAverageVisibility }}</el-descriptions-item>
        <el-descriptions-item label="平均风速">{{ Record?.AverageWindSpeed }}</el-descriptions-item>
        <el-descriptions-item label="平均风速属性">{{ Record?.AttributesOfAverageWindSpeed }}</el-descriptions-item>
        <el-descriptions-item label="最大持续风速">{{ Record?.MaximumSustainedWindSpeed }}</el-descriptions-item>
        <el-descriptions-item label="最大持续风速属性">{{ Record?.AttributesOfMaximumSustainedWindSpeed }}</el-descriptions-item>
        <el-descriptions-item label="最高气温">{{ Record?.HighestTemperature }}</el-descriptions-item>
        <el-descriptions-item label="最高气温属性">{{ Record?.AttributesOfHighestTemperature }}</el-descriptions-item>
        <el-descriptions-item label="最低气温">{{ Record?.LowestTemperature }}</el-descriptions-item>
        <el-descriptions-item label="最低气温属性">{{ Record?.AttributesOfLowestTemperature }}</el-descriptions-item>
        <el-descriptions-item label="降水量">{{ Record?.Precipitation }}</el-descriptions-item>
        <el-descriptions-item label="降水量属性">{{ Record?.AttributesOfPrecipitation }}</el-descriptions-item>
        <el-descriptions-item label="积雪深度">{{ Record?.DepthOfSnow }}</el-descriptions-item>
        <el-descriptions-item label="指示器">{{ Record?.Indicator }}</el-descriptions-item>
      </el-descriptions>

      <template #footer>
        <div class="dialog-footer">
          <el-button @click="DialogShow = false">关闭</el-button>
        </div>
      </template>

    </el-dialog>
  </div>
</template>

<style scoped lang="scss"></style>
