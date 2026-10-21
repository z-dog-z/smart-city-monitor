<template>
  <div>
    <Title :title="title"></Title>
    <div ref="right2" style="height: 280px;margin-top: 15px;width: 100%;"></div>
  </div>
</template>
<script setup>
import Title from './Title.vue';
import { ref, onMounted } from 'vue';
//引入条形图表的构造函数
import { Bar } from '@antv/g2plot';
const title = ref("监测视频");
//声明模板引用
const right2 = ref(null);
//将创建条形图表实例封装在函数中（封装折线图表函数）
const bar = () => {
    const data = [
        { year: '昆山学院浦东软件园市政工程', value: 3 },
        { year: '太原理工大学一号教学楼工程', value: 0 },
        { year: '中北大学', value: 0 },
        { year: '兰州理工大学', value: 0 },
        { year: '测试', value: 0 },
        { year: '一号工程', value: 1 },
    ];

    const bar = new Bar(right2.value, {
        data,
        xField: 'value',
        yField: 'year',
        seriesField: 'year',
        legend: {
            position: 'top', 
            label: {
                style: {
                    fill: 'white', 
                    fontSize: 12
                }
            },
            marker: {
                size: 14
            },
            filter: (item) => {
                const keepItems = ['昆山学院浦东软件园市政工程', '一号工程'];
                return keepItems.includes(item.value);
            }
        },
        // 自定义条形颜色
        color: (datum) => {
            if (datum.year === '昆山学院浦东软件园市政工程') {
                return '#f9c6d0';
            } else if (datum.year === '一号工程') {
                return '#f7d04d';
            }
            return '#e5e5e5';
        },
        // X轴
        xAxis: {
            label: {
                style: {
                    fill: 'white',
                    fontSize: 14,
                },
            },
            min: 0,
            max: 3,
            tickCount: 4
        },
        //y轴
        yAxis: {
            label: {
                style: {
                    fill: 'white',
                    fontSize: 14,
                }
            }
        },
        barSize: 20,
        barStyle: {
            lineWidth: 0
        },
        background: null
    });
    bar.render();
}
onMounted(() => {
    bar();
})
</script>
<style lang="less" scoped></style>