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
    },
    data() {
        return {};
    },
    mounted() {
        this.drawChart(this.id, this.title, this.barData);
    },
    watch: {
        barData(newVal) {
            this.drawChart(this.id, this.title, this.barData);
        },
    },
    methods: {
        random(min, max) {
            return Math.floor(Math.random() * (max - min)) + min;
        },
        drawChart(id, title, data) {
            console.log("data-----------------------", data[0].value.length);
            let myChart = echarts.init(document.getElementById(id));
            let barWidth = 18;
            let color = [];
            let normalColor = "#ffffff";
            let fontSize = 12;
            let xdata = [];
            let yData1 = [];
            let yData2 = [];
            let yData3 = [];
            let yData4 = [];
            let yData5 = [];
            let yData6 = [];
            let yData7 = [];
            let yData8 = [];
            let yData9 = [];
            let yData10 = [];
            let yData11 = [];
            let yData12 = [];
            let yData13 = [];
            let yData14 = [];
            let yData15 = [];
            let yData16 = [];
            let yData17 = [];
            let yData18 = [];
            let yData19 = [];
            let yData20 = [];
            let yData21 = [];
            let yData22 = [];
            let yData23 = [];
            let yData24 = [];
            let yData25 = [];
            let yData26 = [];
            let yData27 = [];
            let yData28 = [];
            let yData29 = [];
            let yData30 = [];
            let yData31 = [];
            let legendData = [
                "用户总数",
                "用户综合评分（10分）",
                "用户综合评分（20分）",
                "用户综合评分（30分）",
                "用户综合评分（40分）",
                "用户综合评分（50分）",
                "用户口味评分（0分）",
                "用户口味评分（1分）",
                "用户口味评分（2分）",
                "用户口味评分（3分）",
                "用户口味评分（4分）",
                "用户环境评分（0分）",
                "用户环境评分（1分）",
                "用户环境评分（2分）",
                "用户环境评分（3分）",
                "用户环境评分（4分）",
                "用户服务评分（0分）",
                "用户服务评分（1分）",
                "用户服务评分（2分）",
                "用户服务评分（3分）",
                "用户服务评分（4分）",
                "用户等级统计（1级）",
                "用户等级统计（5级）",
                "用户等级统计（10级）",
                "用户等级统计（20级）",
                "用户等级统计（30级）",
                "用户等级统计（40级）",
                "用户等级统计（45级）",
                "用户等级统计（50级）",
                "用户等级统计（60级）",
            ];
            window.onresize = function () {
                myChart.resize();
            };
            data.forEach((items, index) => {
                xdata.push(items.name + "月");
                yData1.push(items.value[0]);
                yData2.push(items.value[1]);
                yData3.push(items.value[2]);
                yData4.push(items.value[3]);
                yData5.push(items.value[4]);
                yData6.push(items.value[5]);
                yData7.push(items.value[6]);
                yData8.push(items.value[7]);
                yData9.push(items.value[8]);
                yData10.push(items.value[9]);
                yData11.push(items.value[10]);
                yData12.push(items.value[11]);
                yData13.push(items.value[12]);
                yData14.push(items.value[13]);
                yData15.push(items.value[14]);
                yData16.push(items.value[15]);
                yData17.push(items.value[16]);
                yData18.push(items.value[17]);
                yData19.push(items.value[18]);
                yData20.push(items.value[19]);
                yData21.push(items.value[20]);
                yData22.push(items.value[21]);
                yData23.push(items.value[22]);
                yData24.push(items.value[23]);
                yData25.push(items.value[24]);
                yData26.push(items.value[25]);
                yData27.push(items.value[26]);
                yData28.push(items.value[27]);
                yData29.push(items.value[28]);
                yData30.push(items.value[29]);
                yData31.push(items.value[30]);
            });
            data[0].value.forEach((items, index) => {
                color.push(
                    "rgb(" +
                        this.random(0, 255) +
                        "," +
                        this.random(0, 255) +
                        ",255)"
                );
            });
            myChart.setOption(
                {
                    title: {
                        text: title,
                        top: 0,
                        left: 60,
                        textStyle: {
                            color: "#fff",
                            fontSize: 20,
                        },
                    },
                    color: color,
                    animation: false, //去除加载时缓动动画
                    legend: {
                        type: "scroll",
                        left: "5%",
                        top: "8%",
                        textStyle: {
                            color: "#ffffff",
                            fontSize: 12,
                        },
                        data: legendData,
                        color: color,
                    },
                    grid: [
                        {
                            left: "0%",
                            bottom: "1%",
                            top: "5%",
                            right: "2%",
                            containLabel: true,
                        },
                    ],
                    tooltip: {
                        trigger: "axis",
                        axisPointer: {
                            type: "shadow",
                        },
                    },
                    xAxis: {
                        type: "category",
                        boundaryGap: false,
                        axisLabel: {
                            show: true,
                            textStyle: {
                                color: normalColor, //更改坐标轴文字颜色
                                fontSize: fontSize, //更改坐标轴文字大小
                            },
                        },
                        axisLine: {
                            lineStyle: {
                                color: normalColor, //更改坐标轴颜色
                            },
                        },
                        axisTick: {
                            show: true,
                        },
                        data: xdata,
                    },
                    yAxis: {
                        name: "单位:家",
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
                        axisTick: {
                            show: false,
                        },
                        splitLine: {
                            show: false,
                            lineStyle: {
                                color: "#2d3d53",
                            },
                        },
                    },
                    series: [
                        {
                            name: legendData[0],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[0],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[0],
                            },
                            data: yData1,
                        },
                        {
                            name: legendData[1],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[1],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[1],
                            },
                            data: yData2,
                        },
                        {
                            name: legendData[2],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[2],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[2],
                            },
                            data: yData3,
                        },
                        {
                            name: legendData[3],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[3],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[3],
                            },
                            data: yData4,
                        },
                        {
                            name: legendData[4],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[4],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[4],
                            },
                            data: yData5,
                        },
                        {
                            name: legendData[5],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[5],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[5],
                            },
                            data: yData6,
                        },
                        {
                            name: legendData[6],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[6],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[5],
                            },
                            data: yData7,
                        },
                        {
                            name: legendData[7],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[7],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[7],
                            },
                            data: yData8,
                        },{
                            name: legendData[8],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[8],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[8],
                            },
                            data: yData9,
                        },{
                            name: legendData[9],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[9],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[9],
                            },
                            data: yData10,
                        },{
                            name: legendData[10],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[10],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[10],
                            },
                            data: yData11,
                        },{
                            name: legendData[11],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[11],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[11],
                            },
                            data: yData12,
                        },{
                            name: legendData[12],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[12],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[12],
                            },
                            data: yData13,
                        },
                        {
                            name: legendData[13],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[13],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[13],
                            },
                            data: yData14,
                        },{
                            name: legendData[14],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[14],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[14],
                            },
                            data: yData15,
                        },{
                            name: legendData[15],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[15],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[15],
                            },
                            data: yData16,
                        },{
                            name: legendData[16],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[16],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[16],
                            },
                            data: yData17,
                        },{
                            name: legendData[17],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[17],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[17],
                            },
                            data: yData18,
                        },{
                            name: legendData[18],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[18],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[18],
                            },
                            data: yData19,
                        },{
                            name: legendData[19],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[19],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[19],
                            },
                            data: yData20,
                        },{
                            name: legendData[20],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[20],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[20],
                            },
                            data: yData21,
                        },{
                            name: legendData[21],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[21],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[21],
                            },
                            data: yData22,
                        },{
                            name: legendData[22],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[22],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[22],
                            },
                            data: yData23,
                        },{
                            name: legendData[23],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[23],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[23],
                            },
                            data: yData24,
                        },{
                            name: legendData[24],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[24],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[24],
                            },
                            data: yData25,
                        },{
                            name: legendData[25],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[25],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[25],
                            },
                            data: yData26,
                        },{
                            name: legendData[26],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[26],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[26],
                            },
                            data: yData27,
                        },{
                            name: legendData[27],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[27],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[27],
                            },
                            data: yData28,
                        },{
                            name: legendData[28],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[28],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[28],
                            },
                            data: yData29,
                        },{
                            name: legendData[29],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[29],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[29],
                            },
                            data: yData30,
                        },{
                            name: legendData[30],
                            type: "line",
                            z: 22,
                            smooth: true,
                            symbol: "none",
                            symbolSize: 8,
                            itemStyle: {
                                normal: {
                                    color: color[30],
                                },
                            },
                            label: {
                                normal: {
                                    show: false,
                                    position: "top",
                                    formatter: "C",
                                    textStyle: {
                                        color: "#fff",
                                        fontSize: fontSize,
                                    },
                                },
                            },
                            lineStyle: {
                                width: 2,
                                color: color[30],
                            },
                            data: yData31,
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