<template>
  <div class="online-wrap">
    <div class="online-head-left">城市环境下有毒气体扩散预测及源项反演系统</div>
    <div class="online-head-right">
      <div class="online-head-button">
        <div class="online-head-icon">
          <i class="el-icon-refresh-right"></i>
        </div>
        <div class="online-head-elbutton">
          <el-button
            type="primary"
            size="mini"
            style="position: absolute; left: 12px"
            @click="initAll"
            >刷新</el-button
          >
        </div>
      </div>
      <div class="online-head-button online-head-button1">
        <div class="online-head-icon">
          <i class="el-icon-s-data"></i>
        </div>
        <div class="online-head-elbutton">
          <el-button
            type="primary"
            size="mini"
            @click="dialogTableVisible = true"
            >基础数据</el-button
          >
        </div>
      </div>
      <div class="online-head-button online-head-button2">
        <div class="online-head-icon">
          <i class="el-icon-video-camera-solid"></i>
        </div>
        <div class="online-head-elbutton">
          <el-button
            type="primary"
            size="mini"
            @click="dialogFormVisible = true"
            >源项反演</el-button
          >
        </div>
      </div>
      <div class="online-head-button online-head-button3">
        <div class="online-head-icon">
          <i class="el-icon-aim"></i>
        </div>
        <div class="online-head-elbutton">
          <el-button type="primary" size="mini" @click="result"
            >结果显示</el-button
          >
        </div>
      </div>
      <div class="online-head-button online-head-button4">
        <div class="online-head-icon">
          <i class="el-icon-data-analysis"></i>
        </div>
        <div class="online-head-elbutton">
          <el-button type="primary" size="mini" @click="dataDisposal"
            >数据后处理</el-button
          >
        </div>
      </div>
      <div class="online-head-button online-head-button5">
        <div class="online-head-icon">
          <i class="el-icon-bell"></i>
        </div>
        <div class="online-head-elbutton">
          <el-button type="primary" size="mini" @click="initClock"
            >初始隔离预警</el-button
          >
        </div>
      </div>
      <div class="online-head-button online-head-button6">
        <div class="online-head-icon">
          <i class="el-icon-s-opportunity"></i>
        </div>
        <div class="online-head-elbutton">
          <el-button type="primary" size="mini" @click="openForecast"
            >正向预测</el-button
          >
        </div>
      </div>
      <div class="online-head-button online-head-button7">
        <div class="online-head-icon">
          <i class="el-icon-location-information"></i>
        </div>
        <div class="online-head-elbutton">
          <el-button type="primary" size="mini" @click="openArea"
            >地形数据预处理</el-button
          >
        </div>
      </div>
      <div class="online-head-button online-head-button8">
        <div class="online-head-icon">
          <i class="el-icon-cloudy"></i>
        </div>
        <div class="online-head-elbutton">
          <el-button type="primary" size="mini" @click="openWeather"
            >气象数据预处理</el-button
          >
        </div>
      </div>
      <el-dialog title="源项反演" :visible.sync="dialogFormVisible">
        <el-form :inline="true" ref="form" :model="form" label-width="80px">
          <el-form-item label="项目名称">
            <el-input v-model="form.name"></el-input>
          </el-form-item>
          <el-form-item label="迭代次数">
            <el-input v-model="form.iteration"></el-input>
          </el-form-item>
          <el-form-item label="数据点个数">
            <el-input v-model="form.dataPoint"></el-input>
          </el-form-item>
          <el-form-item label="泄露质量流行初始值(kg/h)">
            <el-input v-model="form.initMass"></el-input>
          </el-form-item>
          <el-form-item label="泄露质量流行最大值(kg/h)">
            <el-input v-model="form.maxMass"></el-input>
          </el-form-item>
          <el-form-item label="泄露质量流行最小值(kg/h)">
            <el-input v-model="form.minMass"></el-input>
          </el-form-item>
          <el-form-item label="泄露源X坐标初始值(Km)">
            <el-input v-model="form.initXpoint"></el-input>
          </el-form-item>
          <el-form-item label="泄露源Y坐标初始值(Km)">
            <el-input v-model="form.initYpoint"></el-input>
          </el-form-item>
          <el-form-item label="泄露源X坐标最大值(Km)">
            <el-input v-model="form.maxXpoint"></el-input>
          </el-form-item>
          <el-form-item label="泄露源Y坐标最大值(Km)">
            <el-input v-model="form.maxYpoint"></el-input>
          </el-form-item>
          <el-form-item label="泄露源X坐标最小值(Km)">
            <el-input v-model="form.minXpoint"></el-input>
          </el-form-item>
          <el-form-item label="泄露源Y坐标最小值(Km)">
            <el-input v-model="form.minYpoint"></el-input>
          </el-form-item>
          <el-form-item label="算法选择" style="width: 600px">
            <el-radio-group v-model="form.algorithm">
              <el-radio label="Metropolis-hastings算法"></el-radio>
              <el-radio label="自适应Metropolis算法"></el-radio>
              <el-radio label="延迟拒绝Metropolis算法"></el-radio>
              <el-radio label="延迟拒绝自适应Metropolis算法"></el-radio>
            </el-radio-group>
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button @click="dialogFormVisible = false">取 消</el-button>
          <el-button type="primary" @click="dialogFormVisible = false"
            >计 算</el-button
          >
        </div>
      </el-dialog>

      <el-dialog title="基础数据" :visible.sync="dialogTableVisible">
        <el-table :data="gridData">
          <el-table-column
            property="material"
            label="材料"
            width="150"
          ></el-table-column>
          <el-table-column
            property="radius"
            label="隔离区半径(m)"
            width="200"
          ></el-table-column>
          <el-table-column
            property="dayLength"
            label="护区长度-白天(Km)"
            width="150"
          ></el-table-column>
          <el-table-column
            property="nightLength"
            label="护区长度-夜晚(Km)"
          ></el-table-column>
        </el-table>
      </el-dialog>
    </div>
    <div class="left-top-table">
      <div class="the-title">
        <div class="the-title-word word-blue">本年度整治任务</div>
      </div>
      <div class="ltt-air-part">
        <div class="ltt-title-word">气体监测进度</div>
        <div style="width: 100px; height: 100px" ref="airTaskChart"></div>
      </div>
      <div class="ltt-area-part">
        <div class="ltt-title-word">区域监测进度</div>
        <div style="width: 100px; height: 100px" ref="areaTaskChart"></div>
      </div>
    </div>
    <div class="left-middle-table">
      <div class="the-title">
        <div class="the-title-word word-blue">当前检测进度</div>
      </div>
      <div class="lmt-first">
        <table class="edit">
          <tbody class="group group1">
            <tr>
              <td>检测站点</td>
              <td>50个</td>
            </tr>
            <tr>
              <td>达标</td>
              <td>30个</td>
            </tr>
            <tr>
              <td>未达标</td>
              <td>20个</td>
            </tr>
          </tbody>
        </table>
        <div
          class="lmt-chart"
          style="width: 75px; height: 75px"
          ref="stationCheckChart"
        ></div>
      </div>
      <div class="lmt-second">
        <table class="edit">
          <tbody class="group">
            <tr>
              <td>主要区域</td>
              <td>11个</td>
            </tr>
            <tr>
              <td>达标</td>
              <td>8个</td>
            </tr>
            <tr>
              <td>未达标</td>
              <td>3个</td>
            </tr>
          </tbody>
        </table>
        <div
          class="lmt-chart"
          style="width: 75px; height: 75px"
          ref="areaCheckChart"
        ></div>
      </div>
      <div class="lmt-third">
        <table class="edit">
          <tbody class="group">
            <tr>
              <td>重点区域</td>
              <td>80个</td>
            </tr>
            <tr>
              <td>达标</td>
              <td>40个</td>
            </tr>
            <tr>
              <td>未达标</td>
              <td>40个</td>
            </tr>
          </tbody>
        </table>
        <div
          class="lmt-chart"
          style="width: 75px; height: 75px"
          ref="highCheckChart"
        ></div>
      </div>
    </div>
    <div class="online-map" style="width:450px height:600px" ref="onlineMap">
      <img
        :src="resultImg"
        style="width:100px height:600px"
        class="result-img"
        v-if="resultVisible"
      />
    </div>
    <div class="right-top-table">
      <div class="the-title">
        <div class="the-title-word word-blue">今日报警信息</div>
      </div>
      <table class="edit edit1">
        <tbody class="group">
          <tr>
            <td>报警站点</td>
            <td>报警时间</td>
            <td>报警原因</td>
          </tr>
          <tr>
            <td>气体检测站1</td>
            <td>2021-5-15 9:05</td>
            <td>二氧化碳浓度超标</td>
          </tr>
          <tr>
            <td>气体检测站2</td>
            <td>2021-5-15 13:23</td>
            <td>二氧化氮浓度超标</td>
          </tr>
          <tr>
            <td>气体检测站3</td>
            <td>2021-5-15 20:15</td>
            <td>二氧化硫浓度超标</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="right-middle-table">
      <div class="the-title">
        <div class="the-title-word word-blue">达标率统计</div>
      </div>
      <div style="width: 300px; height: 245px" ref="rateChart"></div>
    </div>
    <div class="bottom-table">
      <div class="the-title">
        <div class="the-title-word word-blue">实时监测数据</div>
      </div>
      <table class="edit edit2">
        <tbody class="group group-one">
          <tr>
            <td>测站名称</td>
            <td>监测时间</td>
            <td>PH</td>
            <td>CO2(ppm)</td>
            <td>SO2(ug/m3)</td>
            <td>NO2(ug/m3)</td>
            <td>CO(ug/m3)</td>
            <td>O3(ug/m3)</td>
            <td>类型</td>
          </tr>
          <tr>
            <td>气体检测站1</td>
            <td>2021-5-15 9:05</td>
            <td>7</td>
            <td>347</td>
            <td>150</td>
            <td>167</td>
            <td>8</td>
            <td>160</td>
            <td>一级</td>
          </tr>
          <tr>
            <td>气体检测站2</td>
            <td>2021-5-15 13:23</td>
            <td>7</td>
            <td>145</td>
            <td>129</td>
            <td>325</td>
            <td>8</td>
            <td>137</td>
            <td>一级</td>
          </tr>
          <tr>
            <td>气体检测站3</td>
            <td>2021-5-15 20:15</td>
            <td>7</td>
            <td>347</td>
            <td>259</td>
            <td>120</td>
            <td>10</td>
            <td>176</td>
            <td>二级</td>
          </tr>
          <tr>
            <td>气体检测站4</td>
            <td>2021-5-15 22:35</td>
            <td>7</td>
            <td>239</td>
            <td>108</td>
            <td>135</td>
            <td>6</td>
            <td>187</td>
            <td>一级</td>
          </tr>
          <tr>
            <td>气体检测站3</td>
            <td>2021-5-15 20:15</td>
            <td>7</td>
            <td>347</td>
            <td>259</td>
            <td>120</td>
            <td>10</td>
            <td>176</td>
            <td>二级</td>
          </tr>
          <tr>
            <td>气体检测站5</td>
            <td>2021-5-15 16:27</td>
            <td>7</td>
            <td>567</td>
            <td>357</td>
            <td>102</td>
            <td>10</td>
            <td>187</td>
            <td>二级</td>
          </tr>
          <tr>
            <td>气体检测站6</td>
            <td>2021-5-15 23:28</td>
            <td>7</td>
            <td>267</td>
            <td>117</td>
            <td>108</td>
            <td>4</td>
            <td>125</td>
            <td>一级</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
import "echarts/lib/chart/heatmap";
import map from "@/assets/img/地图.jpg";
import result from "@/assets/img/result.jpg";
const echarts = require("echarts/lib/echarts");
require("echarts/lib/chart/gauge");
require("echarts/lib/component/title");
require("echarts/lib/component/toolbox");
require("echarts/lib/component/tooltip");
require("echarts/lib/component/grid");
require("echarts/lib/component/legend");
require("echarts/lib/chart/line");
require("echarts/lib/chart/scatter");
require("echarts/lib/chart/effectScatter");
require("echarts/lib/chart/custom");
export default {
  name: "onlineUse",
  data() {
    return {
      mapImg: map,
      resultImg: result,
      dialogFormVisible: false,
      dialogTableVisible: false,
      resultVisible: false,
      form: {
        name: "",
        iteration: "1000",
        dataPoint: "52",
        initMass: "2500",
        minMass: "1000",
        maxMass: "3500",
        initXpoint: "562.5",
        initYpoint: "4320.42",
        maxXpoint: "565.373",
        maxYpoint: "4321.9",
        minXpoint: "560.373",
        minYpoint: "4218.9",
        algorithm: "",
      },
      gridData: [
        {
          material: "AC",
          radius: "60 m",
          dayLength: "0.1 km",
          nightLength: "0.7 km",
        },
        {
          material: "Adamsite",
          radius: "30 m",
          dayLength: "0.3 km",
          nightLength: "1.0 km",
        },
        {
          material: "Buzz",
          radius: "60 m",
          dayLength: "0.1 km",
          nightLength: "0.3 km",
        },
        {
          material: "BZ",
          radius: "60 m",
          dayLength: "0.4 km",
          nightLength: "1.7 km",
        },
        {
          material: "CA",
          radius: "30 m",
          dayLength: "0.1 km",
          nightLength: "0.4 km",
        },
        {
          material: "CG",
          radius: "150 m",
          dayLength: "0.8 km",
          nightLength: "3.2 km",
        },
        {
          material: "CK",
          radius: "30 m",
          dayLength: "0.2 km",
          nightLength: "1.4 km",
        },
        {
          material: "CN",
          radius: "30 m",
          dayLength: "0.1 km",
          nightLength: "0.2 km",
        },
        {
          material: "CS",
          radius: "30 m",
          dayLength: "0.1 km",
          nightLength: "0.6 km",
        },
        {
          material: "CX",
          radius: "60 m",
          dayLength: "0.2 km",
          nightLength: "1.1 km",
        },
        {
          material: "DA",
          radius: "30 m",
          dayLength: "0.2 km",
          nightLength: "0.8 km",
        },
        {
          material: "DC",
          radius: "30 m",
          dayLength: "0.1 km",
          nightLength: "0.6 km",
        },
      ],
    };
  },
  methods: {
    initAll(){
      this.initChart();
      this.initData();
    },
    initChart() {
      this.initTaskChart();
      this.initCheckChart(
        60,
        this.$refs.stationCheckChart,
        "#1E90FF",
        "#4694cb"
      );
      this.initCheckChart(73, this.$refs.areaCheckChart, "#00BFFF", "#2fc6da");
      this.initCheckChart(50, this.$refs.highCheckChart, "#87CEEB", "#2fc6da");
      this.initRateChart();
      //this.initMap();
    },
    initData(){
      this.resultVisible = false;
    },
    initTaskChart() {
      let airTaskChart = echarts.init(this.$refs.airTaskChart); // 绘制图表
      let areaTaskChart = echarts.init(this.$refs.areaTaskChart);
      var option = {
        series: [
          {
            type: "gauge",
            startAngle: 180,
            endAngle: 0,
            min: 0,
            max: 100,
            splitNumber: 10,
            itemStyle: {
              color: "#FFA500",
              shadowColor: "rgba(0,138,255,0.45)",
              shadowBlur: 0.4,
              shadowOffsetX: 0.4,
              shadowOffsetY: 0.4,
            },
            progress: {
              show: true,
              roundCap: true,
              width: 3.6,
            },
            pointer: {
              show: false,
            },
            axisLine: {
              roundCap: true,
              lineStyle: {
                width: 3.6,
              },
            },
            axisTick: {
              show: false,
            },
            splitLine: {
              show: false,
            },
            axisLabel: {
              show: false,
            },
            title: {
              show: false,
            },
            detail: {
              opacity: 0.6,
              width: "80%",
              lineHeight: 10,
              height: 8,
              borderRadius: 1.6,
              offsetCenter: [0, "-35%"],
              valueAnimation: true,
              fontSize: 10,
              textStyle: { color: "#fff" },
              formatter: function (value) {
                return (
                  "完成进度\n" + "{value|" + value.toFixed(0) + "}{unit|%}"
                );
              },
              rich: {
                value: {
                  fontSize: 12,
                  fontWeight: "bolder",
                  color: "#FFA500",
                },
                unit: {
                  fontSize: 12,
                  color: "#FFA500",
                  padding: [0, 0, -4, 2],
                },
              },
            },
            data: [
              {
                value: 80,
              },
            ],
          },
        ],
      };
      airTaskChart.setOption(option);
      areaTaskChart.setOption(option);
    },
    initCheckChart(rate, refer, lineColor, textColor) {
      let stationCheckChart = echarts.init(refer); // 绘制图表
      const gaugeData = [
        {
          value: rate,
          name: "达标率",
          title: {
            offsetCenter: ["0%", "-25%"],
          },
          detail: {
            valueAnimation: true,
            offsetCenter: ["0%", "25%"],
          },
        },
      ];
      var option = {
        series: [
          {
            type: "gauge",
            startAngle: 90,
            endAngle: -270,
            pointer: {
              show: false,
            },
            progress: {
              show: true,
              overlap: false,
              roundCap: true,
              clip: false,
              itemStyle: {
                color: lineColor,
                borderWidth: 0.125,
                borderColor: "#464646",
              },
            },
            axisLine: {
              lineStyle: {
                width: 5,
              },
            },
            splitLine: {
              show: false,
              distance: 0,
              length: 1.25,
            },
            axisTick: {
              show: false,
            },
            axisLabel: {
              show: false,
              distance: 6.25,
            },
            data: gaugeData,
            title: {
              fontSize: 11.25,
              textStyle: { color: textColor },
            },
            detail: {
              width: 6.25,
              height: 0.875,
              fontSize: 11.25,
              color: textColor,
              formatter: "{value}%",
            },
          },
        ],
      };
      stationCheckChart.setOption(option);
    },
    initRateChart() {
      let rateChart = echarts.init(this.$refs.rateChart);
      var option = {
        title: {
          show: false,
        },
        tooltip: {
          trigger: "axis",
        },
        legend: {
          data: ["检测点1", "检测点2", "检测点3"],
          textStyle: { color: "white" },
        },
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true,
        },
        toolbox: {
          feature: {
            saveAsImage: {},
          },
        },
        xAxis: {
          type: "category",
          boundaryGap: false,
          data: ["1月", "2月", "3月", "4月", "5月", "6月"],
          axisLabel: {
            textStyle: {
              color: "white",
            },
          },
          axisLine: {
            lineStyle: {
              color: "white",
            },
          },
        },
        yAxis: {
          type: "value",
          axisLabel: {
            textStyle: {
              color: "white",
            },
          },
          axisLine: {
            lineStyle: {
              color: "white",
            },
          },
        },
        series: [
          {
            name: "检测点2",
            type: "line",
            smooth: true,
            data: [49, 52, 63, 81, 90, 64],
          },
          {
            name: "检测点3",
            type: "line",
            smooth: true,
            data: [64, 61, 38, 43, 40, 42],
          },
          {
            name: "检测点1",
            type: "line",
            smooth: true,
            data: [20, 40, 23, 40, 32, 24],
          },
        ],
      };
      rateChart.setOption(option);
    },
    initMap() {
      let mapChart = echarts.init(this.$refs.onlineMap);
      mapChart.setOption(option);
    },
    openWeather() {
      const loading = this.$loading({
        lock: true,
        text: "气象数据预处理进行中……",
        spinner: "el-icon-loading",
        background: "rgba(0, 0, 0, 0.7)",
      });
      setTimeout(() => {
        loading.close();
        this.$message({
          message: "气象数据预处理完成!",
          type: "success",
        });
      }, 2000);
    },
    openArea() {
      const loading = this.$loading({
        lock: true,
        text: "地形数据预处理进行中……",
        spinner: "el-icon-loading",
        background: "rgba(0, 0, 0, 0.7)",
      });
      setTimeout(() => {
        loading.close();
        this.$message({
          message: "地形数据预处理完成!",
          type: "success",
        });
      }, 4000);
    },
    openForecast() {
      const h = this.$createElement;
      this.$msgbox({
        title: "正向预测",
        message: h("p", null, [h("span", null, "点击确定运行SCIPUFF.exe")]),
        showCancelButton: true,
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        beforeClose: (action, instance, done) => {
          if (action === "confirm") {
            instance.confirmButtonLoading = true;
            instance.confirmButtonText = "执行中...";
            setTimeout(() => {
              done();
              setTimeout(() => {
                instance.confirmButtonLoading = false;
              }, 300);
            }, 3000);
          } else {
            done();
          }
        },
      }).then((action) => {
        this.$message({
          type: "success",
          message: "运行完毕！",
        });
      });
    },
    initClock() {
      this.$alert("半径:60m 长度:0.3km", "初始隔离预警", {
        confirmButtonText: "确定",
        callback: (action) => {
          this.$message({
            type: "info",
            message: `action: ${action}`,
          });
        },
      });
    },
    dataDisposal() {
      const loading = this.$loading({
        lock: true,
        text: "数据后处理……",
        spinner: "el-icon-loading",
        background: "rgba(0, 0, 0, 0.7)",
      });
      setTimeout(() => {
        loading.close();
        this.$message({
          message: "数据后处理完成!",
          type: "success",
        });
      }, 3000);
    },
    result() {
      this.resultVisible= true;
    },
    sourceInversion() {},
  },
  mounted() {
    this.initChart();
  },
};
</script>
<style scoped>
.online-wrap {
  background: url("~@/assets/img/bg_top_cont2.png") no-repeat center;
  background-size: cover;
  width: 1150px;
  height: 820px;
}
.online-head-left {
  position: absolute;
  top: 30px;
  left: 30px;
  width: 220px;
  font-size: 20px;
  font-family: "黑体";
  text-align: center;
}
.online-head-right {
  position: absolute;
  top: 20px;
  right: 5px;
}
.online-head-button {
  position: absolute;
  right: 0px;
  width: 80px;
  margin: auto;
}
.online-head-button1 {
  position: absolute;
  right: 85px;
}
.online-head-button2 {
  position: absolute;
  right: 170px;
}
.online-head-button3 {
  position: absolute;
  right: 255px;
}
.online-head-button4 {
  position: absolute;
  right: 340px;
}
.online-head-button5 {
  position: absolute;
  right: 425px;
}
.online-head-button6 {
  position: absolute;
  right: 510px;
}
.online-head-button7 {
  position: absolute;
  right: 595px;
}
.online-head-button8 {
  position: absolute;
  right: 680px;
}
.el-button {
  background: rgb(9, 22, 101);
  border-color: rgb(14, 29, 120);
  max-width: 80px;
  white-space: normal;
}
.el-button:hover {
  background: rgb(14, 29, 120);
  box-shadow: 0 12px 16px 0 rgba(0, 0, 0, 0.24),
    0 17px 50px 0 rgba(0, 0, 0, 0.19);
}
.online-head-icon {
  width: 20px;
  height: 30px;
  margin: auto;
  font-size: 20px;
}
.online-head-elbutton {
  width: 100px;
  margin: auto;
}
.online-map {
  position: absolute;
  top: 120px;
  left: 330px;
  width: 450px;
  height: 450px;
  background: url("~@/assets/img/地图.jpg") no-repeat center;
  background-size: cover;
}
.result-img{
  position: absolute;
  top: 120px;
  left: 50px;
  width: 400px;
  height: 300px;
  background: url("~@/assets/img/地图.jpg") no-repeat center;
  background-size: cover;
}
.the-title {
  width: 320px;
  overflow: hidden;
  height: 50px;
  background: url("~@/assets/img/bg_tit.png") no-repeat;
  background-size: contain;
}
.the-title-word {
  float: right;
  margin-top: 12px;
  margin-right: 25px;
  font-size: 13px;
  font-weight: bold;
}
.word-blue {
  color: #4694cb;
}
.left-top-table {
  position: absolute;
  top: 120px;
  width: 350px;
  height: 150px;
}
.ltt-air-part {
  position: absolute;
  left: 30px;
}
.ltt-area-part {
  position: absolute;
  left: 160px;
}
.ltt-title-word {
  margin: auto;
  color: #2fc6da;
  font-weight: bold;
}
.left-middle-table {
  position: absolute;
  top: 270px;
  width: 350px;
  height: 300px;
}
.lmt-first {
  position: absolute;
  top: 60px;
}
.lmt-second {
  position: absolute;
  top: 140px;
}
.lmt-third {
  position: absolute;
  top: 220px;
}
.edit {
  position: absolute;
  top: 10px;
  left: 0px;
  text-align: right;
  width: 150px;
  border-collapse: collapse;
  margin: 0 auto;
}
.edit1 {
  position: absolute;
  top: 40px;
  width: 300px;
  text-align: center;
}
.edit2 {
  position: absolute;
  top: 40px;
  width: 100%;
  text-align: center;
}
.group tr {
  height: 20px;
  color: white;
  font-size: 10px;
}
.group > tr:first-of-type {
  color: #2fc6da;
  font-size: 11px;
}
.group-one > tr:first-of-type {
  color: rgb(216, 214, 214);
  font-size: 11px;
}
.lmt-chart {
  position: absolute;
  left: 200px;
}
.right-top-table {
  position: absolute;
  top: 120px;
  right: 10px;
  width: 350px;
  height: 150px;
}
.right-middle-table {
  position: absolute;
  top: 270px;
  right: 10px;
  width: 350px;
  height: 370px;
}
.bottom-table {
  position: absolute;
  top: 600px;
  width: 100%;
}
</style>
