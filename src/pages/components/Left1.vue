<template>
    <div>
        <!-- 父子组件传值
             1.父组件将传递的数据写入子组件中 
        -->
        <Title :title="title"></Title>
        <!-- 提供图表容器 ref为模板引用 可以快速定位dom元素，跟id差不多 -->
        <div ref="left1" style="height: 150px;margin-top: 15px;"></div>
    </div>
</template>
<script setup>
import Title from './Title.vue';
import { ref,onMounted } from 'vue';
//引入折线图表的构造函数
import { Line } from '@antv/g2plot';
const title = ref("实时温度曲线");
//声明模板引用
const left1 = ref(null);
//将创建折线图表实例封装在函数中（封装折线图表函数）
const loadLine = () => {
    const data = [
        { hour: '03:47', value: 6 },
        { hour: '03:46', value: 4 },
        { hour: '03:45', value: 3.5 },
        { hour: '03:44', value: 6 },
        { hour: '03:43', value: 9 },
        { hour: '03:42', value: 14 },
        { hour: '03:41', value: 7 },
        { hour: '03:40', value: 9 },
        { hour: '03:39', value: 13 },
        { hour: '03:38', value: 1 },
    ];

    const line = new Line(left1.value, {
        data,
        xField: 'hour',
        yField: 'value',
        //折线上的文本
        label: {
          style:{
            fill:'white'
          }
        },
        //配置x轴
        xAxis:{
          label:{
            rotate:-45,
            style:{
              fill:'white',
              fontSize:14,
            }
          }
        },
        //配置y轴
        yAxis:{
          label:{
            style:{
              fill:'white',
              fontSize:18,
            }
          }
        },
        //设置曲线是否平滑
        smooth:true,
        point: {
            size: 5,
            shape: 'circle',
            style: {
                fill: 'white',
                stroke: '#5B8FF9',
                lineWidth: 2,
            },
        },
        //设置动画
        animation: {
        appear: {
          //单折线动画使用wave-in 多折线使用path-in
          animation: 'wave-in',
          duration: 5000,
        },
      },
      //设置提示框
        tooltip: { 
          domStyles:{
            //设置提示框内容
            "g2-tooltip":{
              background:'#147',
              color:'white',
              fontSize:18
            }
          },
          showMarkers: false 
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
//onMounted生命周期才能完成渲染
onMounted(()=>{
  loadLine();
})
</script>
<style lang="less" scoped></style>