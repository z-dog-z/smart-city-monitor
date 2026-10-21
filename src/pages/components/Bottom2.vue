<template>
    <div>
        <Title :title="title"></Title>
        <div ref="bottom2" style="height: 150px;margin-top: 15px;"></div>
    </div>
</template>

<script setup>
import Title from './Title.vue';
import { ref, onMounted } from 'vue';
import { Area } from '@antv/g2plot';
const title = ref("监测月报");
const bottom2 = ref(null);
const initAreaChart = () => {
  const data = [
    { timePeriod: '2025.1', value: 35 },
    { timePeriod: '2025.2', value: 42 },
    { timePeriod: '2025.3', value: 38 },
    { timePeriod: '2025.4', value: 50 },
    { timePeriod: '2025.5', value: 45 },
    { timePeriod: '2025.6', value: 60 },
    { timePeriod: '2025.7', value: 72 },
    { timePeriod: '2025.8', value: 68 },
    { timePeriod: '2025.9', value: 55 },
    { timePeriod: '2025.10', value: 48 },
    { timePeriod: '2025.11', value: 40 },
    { timePeriod: '2025.12', value: 36 },
  ];
  const areaChart = new Area(bottom2.value, {
    data,
    xField: 'timePeriod', 
    yField: 'value',
    height: 150,
    xAxis: {
      range: [0, 1],
      label: {
        rotate: -45,
        style: {
          fill: 'white',
          fontSize: 12,
        }
      },
      tickCount: 12,
    },
    yAxis: {
      style: {
        fill: 'white',
        fontSize: 12,
      }
    },
    smooth: false,
    line: {
      style: {
        stroke: '#5B8FF9',
        lineWidth: 2,
      }
    },
    area: {
      style: {
        fill: 'rgba(91, 143, 249, 0.3)',
      }
    },
    tooltip: {
      showMarkers: true,
      formatter: (datum) => {
        return { name: datum.timePeriod, value: `${datum.value}` };
      }
    },
    animation: {
      appear: {
        duration: 1000,
      }
    }
  });

  areaChart.render();
};
onMounted(() => {
  initAreaChart();
});
</script>
<style lang="less" scoped>
</style>