<template>
    <div class="xk-visualization">
        <div id="particles"></div>
        <my-header></my-header>
        <div class="content">
            <el-row>
                <el-col :span="6" class="rows row-left">
                    <el-col :span="24">
                        <xk-charts :id="'starId'" :title="'店铺星级分类'" :barData="star_rating" :unit="'家'"></xk-charts>
                    </el-col>
                    <el-col :span="24">
                        <xk-double :id="'doubleId'" :title="'其他评分统计'" :barData="other_score" :unit="'家'" :legend="other_type" ></xk-double>
                    </el-col>
                    <el-col :span="24">
                        <xk-charts :id="'reviewId'" :title="'店铺评论数量统计'" :barData="review_count" :unit="'家'"></xk-charts>
                    </el-col>
                </el-col>
                <el-col :span="18" class="rows row-center">
                    <el-col :span="14">
                        <div id="map" style="width: 100%; height: 100%"></div>
                    </el-col>
                    <el-col :span="10">
                        <xk-pie :id="'xkPie'" :title="'店铺类型统计'" :pieData="shop_type"  ></xk-pie>
                    </el-col>
                    <el-col :span="24">
                    <xk-lines :id="'LineId'" :title="'全年用户数据分析'" :barData="monthData"></xk-lines>
                    </el-col>
                </el-col>
            </el-row>
        </div>
    </div>
</template>

<script>
// 粒子动画插件
import particlesJs from "particles.js";
import particlesConfig from "../assets/data/particles.json";
// 原始json数据导入
import item from "../assets/data/item.json";
import userItem from "../assets/data/useritem.json";
// 引入地图JSON数据
import echarts from "echarts";
import mianyang from "../assets/data/mianyang2.json";
// 处理后的业务数据导入
import shop_type_data from "../assets/data/json/shop_type.json";
import star_rating_data from "../assets/data/json/star_rating.json";
import review_count_data from "../assets/data/json/review_count.json";
import other_score_data from "../assets/data/json/other_score.json";
import mapJson from "../assets/data/json/map.json";
import month_data from "../assets/data/json/monthData.json"
// shop_type: [],
// star_rating: [],
// review_count: [],
// 子组件引入
import MyHeader from "./header";
import xkCharts from "./charts";
import xkPie from "./pieCharts";
import xkDouble from "./doubleBar";
import xkLines from "./lines"
export default {
    name: "HelloWorld",
    data() {
        return {
            star_text: ["一星", "二星", "三星", "四星", "五星"],
            review_text: ["<10", "10~39", "40~79", "80~99", "100以上"],
            score_text: ["3分以下", "3~5分", "6~8分", "8分以上"],
            other_type: ["口味评分", "环境评分", "服务评分"],

            // 初始化数据
            typeList: [],
            month: [],
            ratings: [],
            monthData: month_data,
            mapData: mapJson,
            shop_type: shop_type_data,
            star_rating: star_rating_data,
            review_count: review_count_data,
            other_score: other_score_data,
        };
    },
    components: {
        MyHeader,
        xkCharts,
        xkPie,
        xkDouble,
        xkLines
    },
    created() {
        //   注册地图
        echarts.registerMap("mianyang", mianyang);
    },
    watch: {
        mapData(newVal) {
            this.chinaConfigure(this.mapData);
        },
    },
    mounted() {
        this.chinaConfigure(this.mapData);
        particlesJS("particles", particlesConfig);
        //  填充店铺类型及评论总数转为数字
        item.RECORDS.forEach((items, index) => {
            items.item_key_word = items.item_info.split(" ")[0];
            items.review_count = items.review_count.split(" ")[0] * 1;
        });
        //  处理店铺星级分类
        // this.star_text.forEach((star, index) => {
        //     this.star_rating.push({
        //         name: star,
        //         value: item.RECORDS.filter((item, i) => item.star == index + 1)
        //             .length,
        //     });
        // });
        //  处理评论统计数据
        // this.review_text.forEach((review, index) => {
        //     this.review_count.push({
        //         name: review,
        //         value: 0,
        //     });
        // });
        // this.review_count.forEach((items, index) => {
        //     if (index == 0) {
        //         items.value = item.RECORDS.filter(
        //             (items, index) => items.review_count < 10
        //         ).length;
        //     } else if (index == 1) {
        //         items.value =
        //             item.RECORDS.filter(
        //                 (items, index) =>
        //                     items.review_count >= 10 && items.review_count < 40
        //             ).length || 0;
        //     } else if (index == 2) {
        //         items.value =
        //             item.RECORDS.filter(
        //                 (items, index) =>
        //                     items.review_count >= 40 && items.review_count <= 80
        //             ).length || 0;
        //     } else if (index == 3) {
        //         items.value =
        //             item.RECORDS.filter(
        //                 (items, index) =>
        //                     items.review_count >= 80 &&
        //                     items.review_count <= 100
        //             ).length || 0;
        //     } else {
        //         items.value =item.RECORDS.filter((items, index) => items.review_count > 100).length || 0;
        //     }
        // });
        //  店铺类型统计
        // item.RECORDS.forEach((items, index) => {
        //     this.typeList.push(items.item_key_word)
        // });
        // this.typeList=this.unique(this.typeList);
        //  this.typeList.forEach((items,index)=>{
        //      this.shop_type.push({
        //          name:items,
        //          value:0,
        //      })
        //  });
        //  this.shop_type.forEach((shop,index)=>{
        //      shop.value =item.RECORDS.filter((items, index) => items.item_key_word==shop.name).length || 0;
        //  });
        //  其他评分分数统计
        // this.score_text.forEach((items,index)=>{
        //     this.other_score.push({
        //         name:items,
        //         lable:"",
        //         value:[]
        //     })
        // });
        // this.other_score.forEach((items,index)=>{
        //     if(index==0){
        //         items.value=[item.RECORDS.filter((items, index) => items.tast < 3).length,item.RECORDS.filter((items, index) => items.environment < 3).length,item.RECORDS.filter((items, index) => items.service < 3).length]
        //     }else if(index==1){
        //         items.value=[item.RECORDS.filter((items, index) => items.tast >= 3 && items.tast<=5).length,item.RECORDS.filter((items, index) => items.environment >= 3 && items.environment<=5).length,item.RECORDS.filter((items, index) => items.service >= 3 && items.service<=5).length]
        //     }else if(index==2){
        //         items.value=[item.RECORDS.filter((items, index) => items.tast >= 6 && items.tast<=8).length,item.RECORDS.filter((items, index) => items.environment >= 6 && items.environment<=8).length,item.RECORDS.filter((items, index) => items.service >= 6 && items.service<=8).length]
        //     }else if(index==3){
        //         items.value=[item.RECORDS.filter((items, index) => items.tast > 8).length,item.RECORDS.filter((items, index) => items.environment > 8 ).length,item.RECORDS.filter((items, index) => items.service > 8).length]
        //     }
        // });
         // 处理地图数据
            // mianyang.features.forEach((items, index) => {
            //     this.mapData.push({
            //         name: items.properties.name,
            //         value: items.properties.num.split("：")[1] * 1,
            //         num1: items.properties.num1.split("："),
            //         num2: items.properties.num2.split("："),
            //         num3: items.properties.num3.split("："),
            //         num4: items.properties.num4.split("："),
            //         num5: items.properties.num5.split("："),
            //         num6: items.properties.num6.split("："),
            //         num7: items.properties.num7.split("："),
            //         num8: items.properties.num8.split("："),
            //         num9: items.properties.num9.split("："),
            //         num10: items.properties.num10.split("："),
            //         num11: items.properties.num11.split("："),
            //         num12: items.properties.num12.split("："),
            //         num13: items.properties.num13.split("："),
            //         num14: items.properties.num14.split("："),
            //         num15: items.properties.num15.split("："),
            //         num16: items.properties.num16.split("："),
            //         num17: items.properties.num17.split("："),
            //     });
            // });
            // this.mapData = this.mapData.sort(function (a, b) {
            //     return b.value - a.value;
            // });

        // 按月份处理userItem数据
        // userItem.RECORDS.forEach((items, index) => {
        //     this.month.push(items.times.split("-")[0] == "13" || items.times.split("-")[0] == "14"? items.times.split("-")[1]: items.times.split("-")[0]);
        //     this.ratings.push(items.user_rank);
        // });
        // 数据去重
        // this.month = this.unique(this.month);
        // this.ratings = this.unique(this.ratings);

        // this.month.forEach((items, index) => {
        //     this.monthData.push({
        //         name: parseInt(items),
        //         value: [],
        //     });
        // });
        // this.monthData.forEach((item, index) => {
        //     item.value = [
                // 按月统计用户总数
                // userItem.RECORDS.filter((month, index) =>month.times.split("-")[0] == "13" ||month.times.split("-")[0] == "14"? month.times.split("-")[1]: month.times.split("-")[0] == item.name).length,
                // 按月统计用户综合评分
                // rating
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.rating==10).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.rating==20).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.rating==30).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.rating==40).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.rating==50).length,
                
                // // tast
                // userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.tast==0).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.tast==1).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.tast==2).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.tast==3).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.tast==4).length,
                // // environment
                // userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.tast==0).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.tast==1).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.tast==2).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.tast==3).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.tast==4).length,
                // // service
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.service==0).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.service==1).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.service==2).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.service==3).length,
                //  userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.service==4).length,
                //                                                                                                                                                                 //  [1, 30, 10, 40, 5, 60, 45, 20, 50,user_rank
                // userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.user_rank==1).length,
                // userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.user_rank==5).length,
                // userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.user_rank==10).length,
                // userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.user_rank==20).length,
                // userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.user_rank==30).length,
                // userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.user_rank==40).length,
                // userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.user_rank==45).length,
                // userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.user_rank==50).length,
                // userItem.RECORDS.filter((rating, index) =>rating.times.split("-")[0] == "13" ||rating.times.split("-")[0] == "14"? rating.times.split("-")[1]: rating.times.split("-")[0] == item.name && rating.user_rank==60).length,
            // ];
        // });
    },
    //
    methods: {
        //   数组去重
        unique(arr) {
            return Array.from(new Set(arr));
        },
        chinaConfigure(mapData) {
            let myChart = echarts.init(document.getElementById("map")); //这里是为了获得容器所在位置
            window.onresize = myChart.resize;
            let option = {
                 title: {
                        text: "全市店铺分布情况",
                        top: 30,
                        right: 160,
                        textStyle: {
                            color: "#fff",
                            fontSize: 20,
                        },
                    },
                // 进行相关配置
                tooltip: {
                    trigger: "item",
                    backgroundColor: "rgba(5,11,35,0.86)", //通过设置rgba调节背景颜色与透明度
                    formatter: function (params) {
                        return `<div id="plan" style="width:300px;">
            <h4 style="margin:16px;font-size:18px;font-weight:normal;color:#fff;">${params.name}</h4>
            <ul style="margin:16px;color:#fff;width:100%;" class="plan-list">
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>店铺总数：</span>   <span style="color:#439aff;font-size:18px">${params.data.value}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num1[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num1[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num2[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num2[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:14px"><span>${params.data.num3[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num3[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num4[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num4[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num5[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num5[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num6[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num6[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num7[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num7[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num8[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num8[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num9[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num9[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num10[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num10[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num11[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num11[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num12[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num12[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num13[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num13[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num14[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num14[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num15[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num15[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num16[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num16[1]}</span>  <span>家</span></li>
            <li style="color:#c9c9c9;width:50% !important;float: left;font-size:12px"><span>${params.data.num17[0]}：</span>  <span style="color:#439aff;font-size:18px">${params.data.num17[1]}</span>  <span>家</span></li>
            </ul>
            </div>`;
                    },
                },
                visualMap: {
                    left: "20%",
                    top: "70%",
                    inRange: {
                        color: ["#c9e7ff", "#006ec6"],
                    },
                    textStyle:{
                        color:"#fff",
                    }
                },
                geo: {
                    // 这个是重点配置区
                    map: "mianyang", // 表示中国地图
                    roam: false,
                    // width: "100%",
                    height: "100%",
                    label: {
                        normal: {
                            show: false, // 是否显示对应地名
                            textStyle: {
                                color: "rgba(0,0,0,0.4)",
                            },
                        },
                    },
                    itemStyle: {
                        normal: {
                            areaColor: "rgba(255, 255, 255, 0)",
                            borderColor: "rgba(255, 255, 255, 1)",
                            borderWidth: 2,
                        },
                        emphasis: {
                            areaColor: "#f87271",
                            borderWidth: 1,
                            borderColor: "rgba(255, 255, 255, 1)",
                        },
                    },
                },
                series: [
                    {
                        type: "scatter",
                        coordinateSystem: "geo", // 对应上方配置
                    },
                    {
                        type: "map",
                        geoIndex: 0,
                        data: mapData,
                    },
                ],
            };
            myChart.setOption(option, true);
            // this.myChart.on("click", (params) => {
            //     this.value = params.name;
            //     this.myChart.setOption(option, true);
            // });
        },
    },
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.xk-visualization {
    position: relative;
    width: 100%;
    height: 100%;
    background: url(../assets/img/bg.png) center no-repeat;
    background-size: cover;
}
#particles {
    position: absolute;
    width: 100%;
    height: 100%;
}
.content {
    width: 100%;
    height: calc(100% - 107px);
    padding: 0 20px 20px 20px;
    box-sizing: border-box;
}
.el-row {
    width: 100%;
    height: 100%;
    margin: 0 !important;
    margin-bottom: 0px;
    &:last-child {
        margin-bottom: 0;
    }
}
.rows {
    height: 100% !important;
    /* background: #fff; */
}
.el-col {
    height: calc(100% / 3);
}
.bg-purple-dark {
    background: #99a9bf;
}
.bg-purple {
    background: #d3dce6;
}
.bg-purple-light {
    background: #e5e9f2;
}
.grid-content {
    height: 50%;
}
.row-left .el-col {
    height: calc(100% / 3);
}
.row-center .el-col-14,
.row-center .el-col-10{
    height: 60% !important;
}
.row-center .el-col-24{
    height: 40% !important;
}
.plan-list>li{
    width:50% !important;float: left;
}
</style>
