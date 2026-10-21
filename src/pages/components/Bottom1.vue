<template>
    <div>
        <Title :title="title"></Title>
        <div ref="bottom1" style="height: 150px;margin-top: 15px;"></div>
    </div>
</template>
<script setup>
  import Title from './Title.vue';
  import {ref,onMounted} from 'vue';
  // 引入折线图表的构造函数
import { Line } from '@antv/g2plot';
  const title = ref("服务事项概览");
  // 声明模板引用 
const bottom1 = ref(null);
// 将创建折线图表实例封装在函数中 封装折线图表函数 
const loadLine = () => {
    const data = [
        { year: '3:47:07', value: 6 },
        { year: '3:46:07', value: 4 },
        { year: '3:45:07', value: 3.5 },
        { year: '3:44:07', value: 6 },
        { year: '3:43:07', value: 9 },
        { year: '3:42:07', value: 14 },
        { year: '3:41:07', value: 7 },
        { year: '3:40:07', value: 9 },
        { year: '3:39:07', value: 13 },
        { year: '3:38:07', value: 1 },
    ];
    const line = new Line(bottom1.value, {
        data,
        xField: 'year',
        yField: 'value',
        // 折线文本配置项
        label: {
            style: {
                fill: 'white'
            }
        },
        // 配置x轴字段 
        xAxis: {
            label: {
                rotate: -45,
                style: {
                    fill: 'white',
                    fontSize: 14,
                }
            }
        },
        // 配置y轴字段
        yAxis: {
            label: {
                style: {
                    fill: 'white',
                    fontSize: 18,
                }
            }
        },
        // 设置曲线是否平滑 
        smooth: true,
        point: {
            size: 5,
            shape: 'circle',
            style: {
                fill: 'pink',
                stroke: '#6eaf6a',
                lineWidth: 2,
            },
        },
        // 设置动画 
        animation: {
            appear: {
                // 单折线动画使用wave-in
                animation: 'wave-in',
                duration: 5000,
            },
        },
        tooltip: { 
            // 设置提示框内容 
            domStyles:{
                "g2-tooltip":{
                    background:'#147',
                    color:'white',
                    fontSize:18
                }
            },
            showMarkers: true 
        
        },
        state: {
            active: {
                style: {
                    shadowBlur: 4,
                    stroke: '#000',
                    fill: 'red',
                },
            },
        },
        interactions: [{ type: 'marker-active' }],
    });

    line.render();
}
// onMounted生命周期才能完成图表渲染 
onMounted(() => {
    loadLine();
})
</script>
<style lang="less" scoped>

</style>