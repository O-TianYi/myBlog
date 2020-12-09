地图json文件生成地址：

[地图json生成工具（精确到区）](https://hxkj.vip/demo/echartsMap/)

[网址2](http://datav.aliyun.com/tools/atlas/#&lat=36.41639310641063&lng=118.76513097945013&zoom=7.5)

[地图绘制（精确到街道是没有各个轮廓的，需要自己手动瞄）](http://geojson.io/#map=3/22.84/117.77)





echartAPI查看方式：

打开[官网](https://echarts.apache.org/zh/option.html#series-bar.label.formatter),然后点击文档---配置项手册，然后根据各个模块来查找对应存在什么参数。常用的有：

一级属性：

color-----组件颜色数组

title----- 标题组件，包含主标题和副标题。 

 legend ---配置图的标记。

+ formatter
+ type
+ orient----排列方式
+ left、right、bottom、top
+ textStyle-----显示的文字的样式
+ itemWidth、itemHeight标签显示的左边的颜色表示矩形大小

 grid （ 绘图网格 ）-----配置网格是否显示，经常用于设置图形位置。

 xAxis ----设置x轴是否显示单元格，标题，显示的颜色等。

yAxis----设置y轴是否显示单元格，标题，显示的颜色等。

 tooltip（ 提示框 ） ----设置点击对应区域出现的提示区域的样式控制。

+ formatter
+ textStyle

 geo （ 地理坐标系组件 ）----控制地图（map）模块区域和边缘样式控制。

 series （实例）----设置实例的样式，例如需要绘制一个bar，这个bar的样式就在改属性设置。

+ 实例对象



子属性：

label----控制显示标签的样式，例如这个bar上显示对应的数值，这个数值怎么显示就在label上设置。

formatter----格式化，对需要显示的内容进行一层修改，例如传递的值为10，但是需要显示为10%.









#### vue结合echart

组件：

```
<template>
  <div class="elastic h100">
    <div id="echarts" class=" w100 h100" ref="echarts"></div>
  </div>
</template>

<script>
export default {
  props: ["initData", "config"],
  data: () => ({
    myEcharts: null, //echarts实例
    timer: null,
    test: false, //demo模式
    testData: {
      name: ["我", "你", "她"],
      value: [100, 150, 200]
    }
  }),
  mounted() {
    if (this.test) {
      this.createEcharts(this.testData);
    } else {
      this.createEcharts(this.initData);
    }
  },
   beforeDestroy() {
    this.myEcharts.dispose();
    clearInterval(this.timer);
  },
  methods: {
    createEcharts(data) {
      this.myEcharts = this.$echarts.init(this.$refs.echarts);
      // 初始化数据
      const xData = data.name;
      const yData = data.value;
      const dataObj = data.name.map((ele, index) => {
        return {
          name: ele,
          value: data.value[index]
        };
      });
      const option = {
        grid: {
          containLabel: true,
        },
      };
      this.myEcharts.setOption(option);
    }
  }
};
</script>

<style>
</style>
```





动态添加series来表示多个实例：

```
<template>
    <div class="elastic h100">
        <div id="echarts" class=" w100 h100" ref="echarts"></div>
    </div>
</template>

<script>
export default {
    props: ["initData", "config"],
    data: () => ({
        myEcharts: null, //echarts实例
        timer: null,
        test: false, //demo模式
        testData: {
            name: ["我", "你", "她"],
            value: [100, 150, 200],
        },
    }),
    mounted() {
        if (this.test) {
            this.createEcharts(this.testData);
        } else {
            this.createEcharts(this.initData);
        }
    },
    beforeDestroy() {
        this.myEcharts.dispose();
        clearInterval(this.timer);
    },
    methods: {
        createEcharts(data) {
            this.myEcharts = this.$echarts.init(this.$refs.echarts);
            // 初始化数据
            const xData = data.name;
            const yData = data.value;
            const dataObj = data.name.map((ele, index) => {
                return {
                    name: ele,
                    value: data.value[index],
                };
            });
            let legendText = this.config.legendText || ["上年度", "本年度"];
            const option = {
                grid: {
                    containLabel: true,
                },
                grid: {
                    left: "5%",
                    right: "3%",
                    top: "30%",
                    bottom: "3%",
                    containLabel: true,
                },
                legend: {
                    icon: "circle",
                    textStyle: {
                        color: "#fff",
                        fontSize: this.$p(11),
                    },
                    data: legendText,
                    left: "10",
                    top: "5",
                    itemWidth: this.$p(10),
                    itemHeight: this.$p(10),
                },
                yAxis: {
                    show: true,
                    type: "value",
                    data: yData,
                    axisLine: {
                        show: false,
                    },
                    splitLine: {
                        show: false,
                    },
                    axisTick: {
                        show: false,
                    },
                    // 标签
                    axisLabel: {
                        formatter: "{value}",
                        // rotate: 40,
                        color: "#fff",
                        fontSize: this.$p(12),
                        fontStyle: "normal", //其他就斜一点
                    },
                },
                xAxis: {
                    show: true,
                    type: "category",
                    data: xData,
                    axisLine: {
                        show: true,
                        lineStyle: {
                            color: "rgba(255,255,255,0.45)",
                        },
                    },
                    axisTick: {
                        show: true,
                    },
                    axisLabel: {
                        show: true,
                        color: "#fff",
                        fontSize: this.$p(10),
                        rotate: this.config.rotate || 0,
                    },
                },
                // 全局提示配置
                tooltip: {
                    show: true,
                    trigger: "axis",
                    // 坐标轴聚焦,优先级低于轴上的 axisPointer 的配置项（简单项目）
                    axisPointer: {
                        // 对应 lineStyle 和 shadowStyle 和 crossStyle
                        type: "none", // shadow  cross
                        // 动画
                        animationDuration: 500,
                    },
                    // 提示框
                    showContent: true, // 是否显示提示框
                    // renderMode  可以对小程序等 进行更好的支持
                    confine: true, // 提示框是否在gird内， 区域小的情况下非常好用。
                    transitionDuration: 0,
                    textStyle: {
                        fontSize: this.$p(16),
                        lineHeight: this.$p(20),
                    },
                    padding: 5,
                },
                series: [],//动态添加实例对象
            };


			//根据传递的对象属性来对同一种类型的图形实现多个
            let tempVal = [];
            if (this.initData.value) {
                tempVal.push(this.initData.value);
            }
            if (this.initData.value1) {
                tempVal.push(this.initData.value1);
            }
            for (let i = 0; i < tempVal.length; i++) {
                var tempObj = {
                    name: this.config.legendText
                        ? this.config.legendText[i]
                        : "",
                    type: "line",
                    data: tempVal[i],
                    symbol: "circle", // 选择点的样子
                    symbolSize: [this.$p(6), this.$p(6)],
                    label: {
                        show: false,
                        position: this.config.position || "top",
                        textStyle: {
                            color: "#fff",
                            fontSize: this.$p(12),
                        },
                    },
                    // 折线样式
                    lineStyle: {
                        color: this.config.colorList
                            ? this.config.colorList[i]
                            : "#0ACEA2",
                        width: this.$p(2),
                    },
                    // 拐点本身样式
                    itemStyle: {
                        color: this.config.colorList
                            ? this.config.colorList[i]
                            : "#0ACEA2",
                        borderType: "solid",
                        borderWidth: this.$p(1),
                        borderColor: "#fff",
                    },
                };
                option.series.push(tempObj);
            }

            this.myEcharts.setOption(option);
        },
    },
};
</script>

<style>
</style>
```

