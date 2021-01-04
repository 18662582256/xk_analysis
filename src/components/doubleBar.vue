<template>
    <div :id="id" class="charts"></div>
</template>

<script>
import echarts from "echarts";
export default {
    props: {
        id: {
            type: String,
            default: () => {
                return "";
            },
        },
        title: {
            type: String,
            default: () => {
                return "";
            },
        },
        barData: {
            type: Array,
            default: () => {
                return [];
            },
        },
        unit: {
            type: String,
            default: () => {
                return "";
            },
        },
        legend: {
            type: Array,
            default: () => {
                return [];
            },
        },
    },
    data() {
        return {};
    },
    mounted() {
        this.drawChart(
            this.id,
            this.title,
            this.barData,
            this.unit,
            this.legend
        );
    },
    watch: {
        barData(newVal) {
            this.drawChart(
                this.id,
                this.title,
                this.barData,
                this.unit,
                this.legend
            );
        },
    },
    methods: {
        drawChart(id, title, data, unit, legend) {
            let myChart = echarts.init(document.getElementById(id));
            window.onresize = function () {
                myChart.resize();
            };
            let x = [];
            let tast = [];
            let environment = [];
            let service = [];
            data.forEach((items, index) => {
                x.push(items.name);
                tast.push(items.value[0]);
                environment.push(items.value[1]);
                service.push(items.value[2]);
            });
            myChart.setOption(
                {
                    title: {
                        text: title,
                        top: 0,
                        left: 20,
                        textStyle: {
                            color: "#fff",
                            fontSize: 20,
                        },
                    },
                    legend: {
                        data: legend,
                        top: "15%",
                        // right: '10',
                        textStyle: {
                            color: "#fff",
                            fontSize: 12,
                        },
                    },
                    tooltip: {
                        trigger: "axis",
                        axisPointer: {
                            type: "shadow",
                            label: {
                                show: true,
                            },
                        },
                    },
                    barWidth: 15,
                    xAxis: {
                    data: x,
                    axisLine: {
                        lineStyle: {
                            color: "#3d5269",
                        },
                    },
                    axisLabel: {
                        color: "#fff",
                        fontSize: 12,
                    },
                    axisTick:{
                            show:false
                    },
                },
                    yAxis: {
                    name: "单位:"+unit,
                    nameTextStyle: {
                        color: "#fff",
                        fontSize: 12,
                    },
                    axisLine: {
                        lineStyle: {
                            color: "#3d5269",
                        },
                    },
                    axisLabel: {
                        color: "#fff",
                        fontSize: 12,
                    },
                     axisTick:{
                            show:false
                    },
                    splitLine: {
                        show: false,
                        lineStyle: {
                            color: "#2d3d53",
                        },
                    },
                    interval: 500,
                },
                    series: [
                        {
                            type: "bar",
                            name: legend[0],
                            itemStyle: {
                                normal: {
                                    label: {
                                        show: false, //开启显示
                                        position: "right", //在上方显示
                                        textStyle: {
                                            //数值样式
                                            color: "rgba(250,250,250,0.6)",
                                            fontSize: 16,
                                            fontWeight: 600,
                                        },
                                    },
                                    color: new echarts.graphic.LinearGradient(
                                        0,
                                        0,
                                        0,
                                        1,
                                        [
                                            {
                                                offset: 0,
                                                color: "rgba(61,126,235,1)",
                                            },
                                            {
                                                offset: 1,
                                                color: "rgba(61,126,235,0)",
                                            },
                                        ]
                                    ),
                                    borderWidth: 2,
                                    //     barBorderRadius: 15,
                                },
                            },
                            data: tast,
                        },
                        {
                            type: "bar",
                            name: legend[1],
                            itemStyle: {
                                normal: {
                                    label: {
                                        show: false, //开启显示
                                        position: "right", //在上方显示
                                        textStyle: {
                                            //数值样式
                                            color: "rgba(250,250,250,0.6)",
                                            fontSize: 16,
                                            fontWeight: 600,
                                        },
                                    },
                                    color: new echarts.graphic.LinearGradient(
                                        0,
                                        0,
                                        0,
                                        1,
                                        [
                                            {
                                                offset: 0,
                                                color: "rgba(15,197,243,1)",
                                            },
                                            {
                                                offset: 1,
                                                color: "rgba(15,197,243,0)",
                                            },
                                        ]
                                    ),
                                    borderWidth: 2,
                                    //     barBorderRadius: 15,
                                },
                            },
                            data: environment,
                        },
                        {
                            type: "bar",
                            name: legend[2],
                            itemStyle: {
                                normal: {
                                    label: {
                                        show: false, //开启显示
                                        position: "right", //在上方显示
                                        textStyle: {
                                            //数值样式
                                            color: "rgba(250,250,250,0.6)",
                                            fontSize: 16,
                                            fontWeight: 600,
                                        },
                                    },
                                    color: new echarts.graphic.LinearGradient(
                                        0,
                                        0,
                                        0,
                                        1,
                                        [
                                            {
                                                offset: 0,
                                                color: "rgba(15,197,103,1)",
                                            },
                                            {
                                                offset: 1,
                                                color: "rgba(15,197,103,0)",
                                            },
                                        ]
                                    ),
                                    borderWidth: 2,
                                    //     barBorderRadius: 15,
                                },
                            },
                            data: service,
                        },
                    ],
                },
                true
            );
        },
    },
};
</script>

<style scoped>
.charts {
    width: 100%;
    height: 100%;
}
</style>