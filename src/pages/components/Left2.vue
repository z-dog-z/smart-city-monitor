<template>
    <div>
        <Title :title="title"></Title>
        <!-- 设置饼图图标容器 -->
        <div ref="left2" style="height: 150px"></div>
    </div>
</template>
<script setup>
import Title from './Title.vue';
import { ref, onMounted } from 'vue';
//引入饼图的构造函数
import { Pie } from "@antv/g2plot";
const title = ref("设备状态分布");
const left2 = ref(null);
//封装加载饼图函数
const loadPie = () => {
    const data = [
        { type: '在线', value: 3 },
        { type: '离线', value: 7 },
    ];
    const piePlot = new Pie(left2.value, {
        appendPadding: 10,
        data,
        angleField: 'value',
        colorField: 'type',
        radius: 0.8,
        label: {
            style: {
                fill: 'white'
            },
            type: 'outer',
            content: '{name} {value}个',
        },
        interactions: [{ type: 'pie-legend-active' }, { type: 'element-active' }],
        legend: {
            itemName: {
                style: {
                    fill: 'white'
                }
            }
        },
        //颜色的分组
        colorField: 'type', // 部分图表使用 seriesField
        color: ({ type }) => {
            if (type === '在线') {
                return 'pink';
            }
            return 'yellow';
        }
    });

    piePlot.render();
}
onMounted(() => {
    loadPie();
})
</script>
<style lang="less" scoped></style>