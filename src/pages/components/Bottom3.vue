<template>
    <div>
        <Title :title="title"></Title>
         <div ref="bottom3" style="height: 150px;margin-top: 15px;"></div>
    </div>
</template>
<script setup>
  import Title from './Title.vue';
  import {ref,onMounted} from 'vue';
  //引入折线图表的构造函数
  import { Line } from '@antv/g2plot';
  const title = ref("监测点信息");
  //声明模板引用
  const bottom3 = ref(null);
  const loadLine = () => {
    const data = [
        { hour: 'tst', value: 0 },
        { hour: 'PM10', value: 10 },
        { hour: 'PM25', value: 5.5 },
    ];

    const line = new Line(bottom3.value, {
        data,
        xField: 'hour',
        yField: 'value',
        height: 150,
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
        smooth:false,
        point:false,
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
<style lang="less" scoped>

</style>