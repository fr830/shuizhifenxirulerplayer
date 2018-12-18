<template>
  <div class="hello">
    <div class="mnplayer">
      <span>模拟播放</span>
    </div>
    <div class="outbox">
     <div class="bgbox">
       <div class="kdnumbox">
         <div>{{msg[0]}}</div>
         <div>{{msg[1]}}</div>
         <div>{{msg[2]}}</div>
         <div>{{msg[3]}}</div>
         <div>{{msg[4]}}</div>
         <div>{{msg[5]}}</div>
       </div>
        <div class="inbox">
        <div class="block">
          <el-slider :min="0" :max="passTime" :step="step" v-model="sliderValue" v-on:change="sliderChange"></el-slider>
        </div>
     </div>
      </div>
    </div>

    <div class="anoutbox">
      <div class="poutbox">
                  <div
              @click="zhant"
              class="box1 box iconfont icon-winfo-icon-tingzhibofang"
              :class="zdata==1?'bcolor':''"
            ></div>
            <div @click="leftplay" class="box2 box iconfont icon-zuobofang" :class="ldata==1?'bcolor':''"></div>
            <div
              @click="checkplay"
              class="box3 box"
              :class="pdata==0?'iconfont icon-bofangzanting':(pdata==1?'iconfont icon-bofang2':'')"
            ></div>
            <div
              @click="rightplay"
              class="box4 box iconfont icon-youbofang"
              :class="rdata==1?'bcolor':''" style="{cursor:pointer}"
            ></div>
      </div>
      <div class="timeoutbox"><span>时间</span>&nbsp; <span>{{sliderValue}}</span></div>
    </div>
  </div>
</template>

<script>
import "../assets/iconfont/iconfont.css";
export default {
  name: "HelloWorld",
  data() {
    return {
      step:1,
      msg: [],
      pdata: 1,
      zdata: 0,
      ldata: 0,
      rdata: 0,
      sliderValue: 0,
      passTime:5,
      time:1.2
    };
  },
  created() {
    var rulerdata = [];
    for (var i = 0; i <= 5; i++) {
      rulerdata.push(i+".00");
    }
    this.msg = rulerdata;
  },
  methods: {
    PlayAndPauseChange() {
      if(this.pdata==0)
      this.pdata = 1;
      else
      this.pdata = 0;
    },
     Play() {
      this.PlayAndPauseChange();
      this.sliderValue = 0;
      this.interval = window.setInterval(this.Playing, 1000); // this.interval = window.
    },
    Playing() {
      if (this.sliderValue + this.step <= this.passTime) {
        this.sliderValue = this.sliderValue + this.step;
        this.labelValue = this.sliderValue;
        //WindowsEvent.MyDispatchEvent("DiffusionDrawPlaying", this.sliderValue);
      } else {
        //this.isPlay = true;
        this.pdata = 1;
        window.clearInterval(this.interval);
      }
    },
    sliderChange() {
      //WindowsEvent.MyDispatchEvent("DiffusionDrawPlaying", this.sliderValue);
    },
    Pause() {
      this.PlayAndPauseChange();
      window.clearInterval(this.interval);
    },
    Back() {
      //this.isPlay = true;
      this.pdata = 1;
      window.clearInterval(this.interval);
      if (this.sliderValue - this.step >= 0) {
        this.sliderValue = this.sliderValue - this.step;
        this.labelValue = this.sliderValue;
        //WindowsEvent.MyDispatchEvent("DiffusionDrawPlaying", this.sliderValue);
      }
    },
    Next() {
      //this.isPlay = true;
      this.pdata = 1;
      window.clearInterval(this.interval);
      if (this.sliderValue + this.step <= this.passTime) {
        this.sliderValue = this.sliderValue + this.step;
        this.labelValue = this.sliderValue;
        //WindowsEvent.MyDispatchEvent("DiffusionDrawPlaying", this.sliderValue);
      }
    },
    Left() {
      this.sliderValue = Number(this.passTime);
      window.clearInterval(this.interval);
      //WindowsEvent.MyDispatchEvent("DiffusionDrawPlaying", this.sliderValue);
    },
    formatTooltip(val) {
      return val / 100;
    },
    checkplay() {
      if (this.pdata == 0) {
        //this.pdata = 1;
        this.zdata = 0;
        this.ldata = 0;
        this.rdata = 0;
        this.Pause();
      } else if (this.pdata == 1) {
        //this.pdata = 0;
        this.zdata = 0;
        this.ldata = 0;
        this.rdata = 0;
        this.Play();
      }
      
    },
    zhant() {
      this.Left();
      if (this.zdata == 0) {
        this.zdata = 1;
        //this.pdata = 1;
        this.ldata = 0;
        this.rdata = 0;
      } else if (this.zdata == 1) {
        this.zdata = 0;
        //this.pdata = 1;
        this.ldata = 0;
        this.rdata = 0;
      }
    },
    leftplay() {
      this.Back();
      if (this.ldata == 0) {
        this.ldata = 1;
        //this.pdata = 0;
        this.rdata = 0;
        this.zdata = 0;
      } else if (this.ldata == 1) {
        this.ldata = 0;
        //this.pdata = 0;
        this.rdata == 0;
        this.zdata = 0;
      }
    },
    rightplay() {
      this.Next();
      if (this.rdata == 0) {
        this.rdata = 1;
        //this.pdata = 0;
        this.ldata = 0;
        this.zdata = 0;
      } else if (this.rdata == 1) {
        this.rdata = 0;
       // this.pdata = 0;
        this.ldata = 0;
        this.zdata = 0;
      }
    }
  }
};
</script>
<style>
.el-slider__runway {
  width: 344px!important;
  height: 10px!important;
  margin: 0!important;
  background-color: hsl(216, 100%, 99%, 0.1)!important;
  border-radius: 3px!important;
  position: relative!important;
  cursor: pointer!important;
  vertical-align: middle!important;
}
.el-slider__bar {
  width: 344px!important;
  height: 10px!important;
  background-color: rgb(72, 162, 252, 0.1)!important;
  border-top-left-radius: 3px!important;
  border-bottom-left-radius: 3px!important;
  position: absolute!important;
  opacity: 0.1!important;
}
.el-slider__button-wrapper {
  height: 22px!important;
    width: 10px!important;
  top: 0px!important;
}
/* .el-slider__button {
    width: 8px;
    height: 56px;
    border-radius: 0%;
} */
.el-slider__button {
   width: 16px!important;
    height: 16px!important;
    border: 0px!important;
  border-radius: 0%!important;
  position: relative;
  border-style: none!important;
  border-color: #ffffff transparent!important;
  background-color: rgb(255, 253, 253, 0.1)!important; 
}

.el-slider__button:hover {
  border-radius: 0%!important;
  position: relative!important;
 /*  top:-16px!important; */
  width: 10px!important;
  border-style: none!important;
  border-color: #ffffff transparent!important;
  background-color: rgb(255, 253, 253, 0.1)!important;
}
.el-slider__button:before {
  content: url("../assets/03.png")!important;
  position: absolute!important;
  height: 0!important;
  width: 0!important;
  top: -12px!important;
  left: 0px!important;

}
.el-slider__button:hover {
  -webkit-transform: scale(1)!important; 
   -ms-transform: scale(1)!important;  
   transform: scale(1)!important;
}
</style>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content:flex-start;
  align-items: center;
  width: 492px;
  height: 195px;
  border: 1px #d1d1da solid;
  margin: 0px 500px;
}
.mnplayer{
  width: 492px;
  height: 40px;
 display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: flex-start;
  align-items: center;
}
.mnplayer>span{
  margin:10px 0px 0px 20px;
  font-size:12px;
  font-family:"微软雅黑";
  color:#6e7b8b;
}
.outbox {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  width: 492px;
  height: 20px;
  margin-top:40px
}
.bgbox{
   display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
   width: 382px;
  height: 64px;
    background-color: #f0f0f1;
}
.kdnumbox{
   width: 360px;
  height: 10px;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content:space-between;
  align-items: center;
  margin-bottom:20px;
  margin-right:10px;
  font-size:12px;
  font-family:"微软雅黑";
  color:#6e7b8b;
}
.inbox {
  width: 356px;
  height: 10px;
    background-image: url("../assets/kdc.png");
  background-repeat: no-repeat;
  }
.anoutbox {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content:space-between;
  align-items: center;
  width: 492px;
  height: 60px;
  /*   background-color: aqua; */
  margin-bottom: -30px;
  margin-top:30px
}
.poutbox{
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: flex-start;
  align-items: center;
margin-left:52px;
}
.box {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: flex-start;
  align-items: center;
  width: 20px;
  height: 20px;
  /* background-color: rgb(57, 223, 84); */
 /*  margin: 0 20px; */
}
.box1{
  margin-right:15px;
}
.box2{
  margin-right:15px;
}
.box3{
  margin-right:15px;
}
.icon-bofang2 {
  color: rgb(48, 100, 241);
}
.bcolor {
  color: rgb(48, 100, 241);
}
.timeoutbox{
  margin-right:52px;
}
.timeoutbox>span{
  font-size:12px;
  font-family:"微软雅黑";
  color:#6e7b8b;
}
.iconfont{
  color:#6e7b8b
}








</style>
