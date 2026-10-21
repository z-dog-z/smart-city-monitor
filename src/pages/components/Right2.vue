<template>
    <div>
        <Title :title="title"></Title>
        <div ref="right2" style="height: 150px;margin-top: 15px;"></div>
    </div>
</template>
<script setup>
import Title from './Title.vue';
import { ref, onMounted } from 'vue';
//引入条形图表的构造函数
import { Bar } from '@antv/g2plot';
const title = ref("实时颗粒物曲线");
//声明模板引用
const right2 = ref(null);
//将创建条形图表实例封装在函数中（封装折线图表函数）
const bar = () => {
    const data = [
        { year: '1951 年', value: 38 },
        { year: '1952 年', value: 52 },
        { year: '1956 年', value: 61 },
        { year: '1957 年', value: 145 },
        { year: '1958 年', value: 48 },
    ];

    const bar = new Bar(right2.value, {
        data,
        xField: 'value',
        yField: 'year',
        seriesField: 'year',
        legend: {
            position: 'top-left',
        },
        xAxis: {
            label: {
                style: {
                    fill: 'white',
                    fontSize: 14,
                },
            }
        },
        yAxis: {
            label: {
                style: {
                    fill: 'white',
                    fontSize: 14,
                }
            }
        },
    });

    bar.render();

}
onMounted(() => {
    bar();
})
</script>
<style lang="less" scoped></style>