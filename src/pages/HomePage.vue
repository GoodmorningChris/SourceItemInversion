<template>
  <el-container>
    <el-header style="text-align:left;color: black;font-size: 30px;font-weight: bolder">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;城&nbsp;市&nbsp;污&nbsp;染&nbsp;气&nbsp;体&nbsp;扩&nbsp;散&nbsp;快&nbsp;速&nbsp;预&nbsp;测&nbsp;系&nbsp;统</el-header>
    <br>
    <el-main>
      <el-menu
        :default-active="tabindex"
        class="el-menu-demo"
        mode="horizontal"
        @select="handleSelect"
        background-color="#213F84"
        text-color="#fff"
        active-text-color="#ffd04b"
        style="width: 1200px;left: 150px"
      >
        <el-menu-item index="1">新闻事件</el-menu-item>
        <el-menu-item index="2">在线使用</el-menu-item>
        <el-menu-item index="3">使用教程</el-menu-item>
        <el-menu-item index="4">安装包下载</el-menu-item>
      </el-menu>
      <div v-if="tabindex==='1'" id="container" style="position:absolute;left: 200px;">
        <div style="display: inline-block">
          <!--        放图片-->
          <br>
          <h3 style="color: black">时事热点</h3>
          <div style="float:left;width: 450px;height: 350px">
            <img :src="imgurl1" style="width: 210px;height: 160px;">
            <img :src="imgurl2" style="width: 210px;height: 160px;"><br>
            <img :src="imgurl3" style="width: 210px;height: 160px;">
            <img :src="imgurl1" style="width: 210px;height: 160px;">
          </div>

          <!--        文字连接-->
          <div style="float:left;width: 500px;height: 350px">

            <el-link href="https://www.sohu.com/a/494127756_121172570" style="font-size: 18px">· 关于宁夏某车间10.5静电爆炸事故，化学原料爆炸产生有害气体该如何防范？</el-link><br><br>
            <el-link href="https://www.shangyici.com/vehicle_464271#:~:text=%E5%A4%A9%E6%B4%A5%E5%A1%98%E6%B2%BD%E5%A4%A7%E7%88%86%E7%82%B8%E8%B5%B7,%E7%AE%A1%E7%90%86%EF%BC%8C%E8%B5%B7%E7%81%AB%E7%88%86%E7%82%B8%E3%80%82" style="font-size: 18px">· 2015年天津塘沽爆炸案，165人遇难身亡,其中99名都是消防员</el-link><br><br>
            <el-link href="https://new.qq.com/omn/20210425/20210425A0D24W00.html" style="font-size: 18px">· 福岛核事故的悲剧遗产-放射性土壤、核泄漏，影响一直在持续？</el-link><br><br>
            <el-link href="https://new.qq.com/omn/20210630/20210630A0237J00.html" style="font-size: 18px">· 大连7·16爆炸纪实：储油罐密布，周边燃起大火，消防员与死神交手</el-link><br><br>
            <el-link href="https://www.lawtime.cn/zhishi/a104390.html" style="font-size: 18px">· 吉化公司爆炸事故中应急预案的经验与教训</el-link><br><br>
            <el-link href="https://www.163.com/dy/article/G86U5CG60511C42J.html" style="font-size: 18px">· 惨剧！4死6伤！黑龙江一化工厂发生中毒事故！</el-link><br><br>
            <el-link href="https://www.thepaper.cn/newsDetail_forward_14478153" style="font-size: 18px">· 扑救82小时，损失3872.1万元，沧州南大港区油罐大火6人被追究刑事责任</el-link><br><br>
            <el-link href="https://news.sohu.com/a/504513344_120099902" style="font-size: 18px">· 江苏响水“3.21”化工厂爆炸事故分析报告</el-link><br><br>


          </div>
        </div>
        <el-divider></el-divider>
<!--        聚焦事件-->
        <h3 style="color: black">聚焦事件</h3>
        <div>
          <el-card style="float: left">
            <div style="width: 350px;color: black;overflow: hidden;word-break:break-all;white-space:normal;
          word-wrap:break-word;"> &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
              9月28日上午1100左右，世界第一大化学品航运公司STOLT TANKERS BV旗下一艘名为 STOLT GROENLAND，43,478-dwt，2009年建造的化学品船在靠泊韩国蔚山港作业时发生重大爆炸事故！（当时报道：重大事故！世界第一大化学品船东所属货船爆炸）
              该事故最终造成两名海员和 15 名岸上工人受伤
            </div><br>
            <img :src="imgurl4" style="width: 350px;height: 200px;">
          </el-card>

          <el-card style="float: left">
            <div style="width: 350px;color: black;overflow: hidden;word-break:break-all;white-space:normal;
          word-wrap:break-word;"> &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
              2013年4月，南京某高校一处废弃实验室发生爆炸，事故造成1死3伤。事故发生直接原因是外来施工人员用明火切割金属，而该废弃实验室是10多年前存放化学药品的实验室。废弃了10多年的实验室，还存放有危险化学品，可以说这起事故，与危险化学品管理疏忽不无关系。
            </div><br>
            <img :src="imgurl5" style="width: 350px;height: 200px;">
          </el-card>
          <el-card style="float: left">
            <div style="width: 350px;color: black;overflow: hidden;word-break:break-all;white-space:normal;
          word-wrap:break-word;"> &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
              3月21日14时48分许，江苏盐城市响水县陈家港镇天嘉宜化工有限公司化学储罐发生爆炸事故，并波及周边16家企业。经全力处置，现场明火已被扑灭，空气污染物指标在许可范围内。
            </div><br>
            <img :src="imgurl6" style="width: 350px;height: 200px;">
          </el-card>
        </div>
      </div>

      <div v-if="tabindex==='2'" style="position:absolute;left: 200px;">
        <br>
        <online-use></online-use>
      </div>

      <div v-if="tabindex==='3'" style="position:absolute;left: 200px;">
        <br>
        <div style="width: 1100px">
          <el-tabs v-model="activeName" @tab-click="handleClick">
            <el-tab-pane label="初始隔离预警" name="first">
              <video    :preload="preload"
                        :height="height" :width="width" align="center" :controls="controls"  :autoplay="autoplay">
                <source :src="videoSrc1" type="video/mp4">
              </video>
            </el-tab-pane>
            <el-tab-pane label="地形数据预处理" name="second">
              <video    :preload="preload"
                        :height="height" :width="width" align="center" :controls="controls"  :autoplay="autoplay">
                <source :src="videoSrc2" type="video/mp4">
              </video>
            </el-tab-pane>
            <el-tab-pane label="基础数据" name="third">
              <video    :preload="preload"
                        :height="height" :width="width" align="center" :controls="controls"  :autoplay="autoplay">
                <source :src="videoSrc3" type="video/mp4">
              </video>
            </el-tab-pane>
            <el-tab-pane label="气象数据预处理" name="fourth">
              <video    :preload="preload"
                        :height="height" :width="width" align="center" :controls="controls"  :autoplay="autoplay">
                <source :src="videoSrc4" type="video/mp4">
              </video>
            </el-tab-pane>
            <el-tab-pane label="源项反演" name="fifth">
              <video    :preload="preload"
                        :height="height" :width="width" align="center" :controls="controls"  :autoplay="autoplay">
                <source :src="videoSrc5" type="video/mp4">
              </video>
            </el-tab-pane>
            <el-tab-pane label="结果显示" name="sixth">
              <video    :preload="preload"
                        :height="height" :width="width" align="center" :controls="controls"  :autoplay="autoplay">
                <source :src="videoSrc6" type="video/mp4">
              </video>
            </el-tab-pane>
            <el-tab-pane label="防护指导" name="seventh">
              <video    :preload="preload"
                        :height="height" :width="width" align="center" :controls="controls"  :autoplay="autoplay">
                <source :src="videoSrc7" type="video/mp4">
              </video>
            </el-tab-pane>
            <el-tab-pane label="新建项目" name="eighth">
              <video    :preload="preload"
                        :height="height" :width="width" align="center" :controls="controls"  :autoplay="autoplay">
                <source :src="videoSrc8" type="video/mp4">
              </video>
            </el-tab-pane>
            <el-tab-pane label="时间设置" name="ninth">
              <video    :preload="preload"
                        :height="height" :width="width" align="center" :controls="controls"  :autoplay="autoplay">
                <source :src="videoSrc9" type="video/mp4">
              </video>
            </el-tab-pane>
            <el-tab-pane label="气象设置" name="tenth">
              <video    :preload="preload"
                        :height="height" :width="width" align="center" :controls="controls"  :autoplay="autoplay">
                <source :src="videoSrc10" type="video/mp4">
              </video>
            </el-tab-pane>
            <el-tab-pane label="物质材料与污染物释放设置" name="eleventh">
              <video    :preload="preload"
                        :height="height" :width="width" align="center" :controls="controls"  :autoplay="autoplay">
                <source :src="videoSrc11" type="video/mp4">
              </video>
            </el-tab-pane>
            <el-tab-pane label="计算域设置" name="twelfth">
              <video    :preload="preload"
                        :height="height" :width="width" align="center" :controls="controls"  :autoplay="autoplay">
                <source :src="videoSrc12" type="video/mp4">
              </video>
            </el-tab-pane>
          </el-tabs>
        </div>

        <div>
          <!--
          <video :src="videoSrc" :poster="videoImg" :autoplay="playStatus" height="421" width="700" :muted="muteStatus">
            your browser does not support the video tag
          </video>
          <button @click="playClick" :class="{hide: isPlay}">点击播放</button> -->
          <!--class="video-js vjs-default-skin vjs-big-play-centered" -->

        </div>
<!--        <video-->
<!--          id="myVideo"-->
<!--          class="video-js"-->
<!--        >-->
<!--          <source-->
<!--            src="//vjs.zencdn.net/v/oceans.mp4"-->
<!--            type="video/mp4"-->
<!--          >-->
<!--        </video>-->
      </div>
    </el-main>
  </el-container>
</template>

<script>

import img1 from '@/assets/img/山东莘县化工厂.jpeg'
import img2 from '@/assets/img/天津塘沽.png'
import dp from '@/assets/img/中心界面.jpg'
import img3 from '@/assets/img/青岛输油管.png'
import img4 from '@/assets/jujiao/左下1.jpg'
import img5 from '@/assets/jujiao/中.png'
import img6 from '@/assets/jujiao/右下.jpg'

import video1 from '@/assets/video/初始隔离预警.mp4'
import video2 from '@/assets/video/地形数据预处理.mp4'
import video3 from '@/assets/video/基础数据.mp4'
import video4 from '@/assets/video/气象数据预处理.mp4'
import video5 from '@/assets/video/源项反演.mp4'
import video6 from '@/assets/video/结果显示.mp4'
import video7 from '@/assets/video/防护指导.mp4'

import video8 from '@/assets/video2/新建项目.mp4'
import video9 from '@/assets/video2/时间设置.mp4'
import video10 from '@/assets/video2/气象设置.mp4'
import video11 from '@/assets/video2/物质材料与污染物释放设置.mp4'
import video12 from '@/assets/video2/计算域设置.mp4'

// import { videoPlayer } from 'vue-video-player'
// import 'video.js/dist/video-js.css'

//在线使用组件引用
import onlineUse from '@/component/onlineUse.vue'
import OnlineUse from "../component/onlineUse";
export default {
  name: "HomePage",
  components: {OnlineUse},
  data(){
      return{
        activeName:'first',
        activeIndex: '1',
        activeIndex2: '1',
        imgurl1:img1,
        imgurl2:img2,
        imgurl3:img3,
        imgurl4:img4,
        imgurl5:img5,
        imgurl6:img6,
        daping:dp,
        tabindex:'1',

        videoSrc1: video1,
        videoSrc2: video2,
        videoSrc3: video3,
        videoSrc4: video4,
        videoSrc5: video5,
        videoSrc6: video6,
        videoSrc7: video7,
        videoSrc8: video8,
        videoSrc9: video9,
        videoSrc10: video10,
        videoSrc11: video11,
        videoSrc12: video12,

        videoImg: img1,
        playStatus: '',
        muteStatus: '',
        isMute: true,
        isPlay: false,
        width: '1000', // 设置视频播放器的显示宽度（以像素为单位）
        height: '600', // 设置视频播放器的显示高度（以像素为单位）
        preload: 'auto', //  建议浏览器是否应在<video>加载元素后立即开始下载视频数据。
        controls: true, // 确定播放器是否具有用户可以与之交互的控件。没有控件，启动视频播放的唯一方法是使用autoplay属性或通过Player API。
        autoplay: ''
      };
  },
  // mounted() {
  //   this.initVideo();
  // },
  methods:{
    handleClick(tab, event) {
      console.log(tab, event);
    },
    handleSelect(key, keyPath) {
      this.tabindex=key;
    if(key==="4"){
         this.downloadEvt('https://github.com/GoodmorningChris/openalpr/archive/refs/heads/master.zip')
      }
    },
    downloadEvt(url, fileName = '未知文件') {
      console.log("ssss")
      const el = document.createElement('a');
      el.style.display = 'none';
      el.setAttribute('target', '_blank');
      /**
       * download的属性是HTML5新增的属性
       * href属性的地址必须是非跨域的地址，如果引用的是第三方的网站或者说是前后端分离的项目(调用后台的接口)，这时download就会不起作用。
       * 此时，如果是下载浏览器无法解析的文件，例如.exe,.xlsx..那么浏览器会自动下载，但是如果使用浏览器可以解析的文件，比如.txt,.png,.pdf....浏览器就会采取预览模式
       * 所以，对于.txt,.png,.pdf等的预览功能我们就可以直接不设置download属性(前提是后端响应头的Content-Type: application/octet-stream，如果为application/pdf浏览器则会判断文件为 pdf ，自动执行预览的策略)
       */
      fileName && el.setAttribute('download', fileName);
      el.href = url;
      console.log(el);
      document.body.appendChild(el);
      el.click();
      document.body.removeChild(el);
    },
    // initVideo() {
    //   //初始化视频方法
    //   let myPlayer = this.$video(myVideo, {
    //     //确定播放器是否具有用户可以与之交互的控件。没有控件，启动视频播放的唯一方法是使用autoplay属性或通过Player API。
    //     controls: true,
    //     //自动播放属性,muted:静音播放
    //     autoplay: "muted",
    //     //建议浏览器是否应在<video>加载元素后立即开始下载视频数据。
    //     preload: "auto",
    //     //设置视频播放器的显示宽度（以像素为单位）
    //     width: "1200px",
    //     //设置视频播放器的显示高度（以像素为单位）
    //     height: "800px"
    //   });
    //}
  }
}
</script>

<style scoped>
.el-header {
  color: #333;
  text-align: center;
  line-height: 100px;
  /*background-color: rgb(0,14,75);*/
}

.el-main {
  color: white;
}
#container {
  /*background-color: red;*/
  white-space: nowrap;
}
.lable {
  /*background-color: white;*/
  display: inline-block;
}
/*.el-tabs__item{*/
/*  height: 60px;*/
/*  color: white !important;*/
/*  text-align: center;*/
/*  padding-top: 10px;*/
/*  font-size: 25px !important;*/
/*  background-color: white !important;*/
/*}*/
/*.is-active{*/
/*  color: white !important;*/
/*  background-color: white !important;*/
/*}*/
</style>
