<template>
    <div>
        <Title :title="title"></Title>
        <div ref="right1" style="height: 150px;margin-top: 15px;"></div>
    </div>
</template>
<script setup>
import Title from './Title.vue';
import { ref, onMounted } from 'vue';
//引入折线图表的构造函数
import { Line } from '@antv/g2plot';
const title = ref("实时湿度曲线");
//声明模板引用
const right1 = ref(null);
//将创建折线图表实例封装在函数中（封装折线图表函数）
const manyloadLine = () => {
    const data = [
        { year: '10:10', temperature: 30, humidity: 5 },
        { year: '10:11', temperature: 29, humidity: 8 },
        { year: '10:12', temperature: 28, humidity: 7 },
        { year: '10:13', temperature: 29, humidity: 10 },
        { year: '10:14', temperature: 31, humidity: 15 },
        { year: '10:15', temperature: 30, humidity: 12 },
        { year: '10:16', temperature: 28, humidity: 18 },
        { year: '10:17', temperature: 32, humidity: 15 },
    ].flatMap(item => [
        { year: item.year, value: item.temperature, category: 'temperature' },
        { year: item.year, value: item.humidity, category: 'humidity' },
    ]);

    const line = new Line(right1.value, {
        data,
        xField: 'year',
        yField: 'value',
        seriesField: 'category',
        smooth: false,
        //动画
        animation: {
            appear: {
                animation: 'path-in',
                duration: 5000,
            },
        },
        //图例在顶部
        legend: {
            position: 'top',
            itemName: {
                style: {
                    fill: 'white',
                },
            },
        },
        //x轴
        xAxis: {
            label: {
                style: {
                    fill: 'white',
                    fontSize: 14,
                },
            },
            line: {
                style: {
                    stroke: 'rgba(255,255,255,0.3)',
                },
            },
        },
        //y轴
        yAxis: {
            label: {
                style: {
                    fill: 'white',
                    fontSize: 18,
                }
            }
        },
        //提示框
        tooltip: {
            domStyles: {
                'g2-tooltip': {
                    background: 'rgba(0,0,0,0.7)',
                    color: 'white',
                },
            },
        },
    });

    line.render();
};
onMounted(() => {
    manyloadLine();
})
</script>
<style lang="less" scoped></style>