<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-lx-favor"></i> schart图表</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="container">
            <div id="myChartBar" class="myChart"></div>
            <div id="myChartPie" class="myChart"></div>
        </div>
    </div>
</template>

<script>
    import echarts from 'echarts';
    export default {
        name: 'basecharts',
        data: () => ({
            lineData :["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"],
            lineData1 :[5, 20, 36, 10, 10, 20],
            PieData :["短袖", "休闲裤", "连衣裙", "外套", "羽绒服"],
            PieData1 : [
                {name:'短袖',value:3200},
                {name:'休闲裤',value:1222},
                {name:'连衣裙',value:2283},
                {name:'外套',value:1314},
                {name:'羽绒服',value:2314}
            ]
        }),
        mounted() {
            this.drawLineBar();
            this.drawLinePie();
        },
        methods: {
            drawLineBar() {
            // 基于准备好的dom，初始化echarts实例
            let myChartBar = echarts.init(document.getElementById('myChartBar'))
            // 绘制柱状图
            myChartBar.setOption({
                title: { text: '柱状图' ,left:'center'},
                tooltip: {},
                xAxis: {
                  data: this.lineData
                },
                yAxis: {},
                series: [{
                  name: '销量',
                  type: 'bar',
                  data: this.lineData1
                }]
             });
            },
            drawLinePie() {
            // 基于准备好的dom，初始化echarts实例
            let myChartPie = echarts.init(document.getElementById('myChartPie'))
            // 绘制饼状图
            myChartPie.setOption({
                title: { text: '饼状图' ,left:'center'},
                tooltip: {
                    trigger: 'item',
                    formatter: "{a} <br/>{b} : {c} ({d}%)"
                },
                legend: {
                    orient: 'vertical',
                    left: 'left',
                    data: this.PieData
                },
                series: [
                  {
                    name: '销量',
                    type: 'pie',
                    radius: '55%',
                    center: ['50%', '60%'],
                    data: this.PieData1,
                    itemStyle: {
                        emphasis: {
                        shadowBlur: 10,
                        shadowOffsetX: 0,
                        shadowColor: 'rgba(0, 0, 0, 0.5)'
                        }
                    }
                  }
                ]
            });
          }
        }
    }
</script>

<style scoped>
.myChart{
    width: 600px;
    height: 450px;;
}    
.container{
    display: flex;
    flex-direction: row;
}   
</style>