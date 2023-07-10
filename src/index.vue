<!-- 核心功能页 -->
<template>
  <div id="app">
    <Header></Header>
    <div class="content">
      <div class="content-title">
        <h1>Gradient Maker</h1>
      </div>
      <div class="content-desc">
        Create and export beautiful gradients.
      </div>
      <!-- 核心功能 -->
      <div class="console">
        <div class="console-seting">
          <GradientMakerSlider ref="gradient" :color1Data="color1Data" :color2Data="color2Data" @getGradient="returnGradient"
            @getClickColor="getClickColor"></GradientMakerSlider>
          <!-- 表单修改 修改渐变色 点击如果为color1 显示 -->
          <div class="color-info" v-if="currColor == 'color1'">
            <div class="color-info-item">
              <p>Color</p>
              <div style="display: flex;align-items: center;">
              <input class="color-input" type="text" v-model="color1Data.color">
              <input class="color-eye" type="color" v-model="color1Data.color">
            </div>
            </div>
            <div class="color-info-item">
              <p>postion</p>
              <input class="color-input" type="number" min="0" max="100" v-model="color1Data.postion">
            </div>
            <div class="color-info-item">
              <p>Rotation</p>
              <input class="color-input" type="text" v-model="color1Data.rotaion">
            </div>
            <div class="color-info-item">
              <p>type</p>
              <select  class="color-input" v-model="color1Data.type">
                <option value="linear">linear</option>
                <option value="radial">radial</option>
              </select>
            </div>
          </div>
          <!-- 表单修改 修改渐变色 点击如果为color2 显示 -->
          <div class="color-info" v-if="currColor == 'color2'">
            <div class="color-info-item">
              <p>Color</p>
              <div style="display: flex;align-items: center;">
              <input class="color-input" type="text" v-model="color2Data.color">
              <input class="color-eye" type="color" v-model="color2Data.color">
            </div>
            </div>
            <div class="color-info-item">
              <p>postion</p>
              <input class="color-input" type="number" min="0" max="100" v-model="color2Data.postion">
            </div>
            <div class="color-info-item">
              <p>Rotation</p>
              <input class="color-input" type="text" v-model="color2Data.rotaion">
            </div>
            <div class="color-info-item">
              <p>type</p>
              <select class="color-input" v-model="color2Data.type" >
                <option value="linear">linear</option>
                <option value="radial">radial</option>
              </select>
            </div>
            
          </div>
          
      <div class="BtnGroup">
        <div class="btn-random" @click="randomFun">
            Random
        </div>
        <div class="btn-Copy" @click="()=>{
          this.show = true
        }">
            Copy
        </div>
      </div>
        </div>
        <div class="color-preview">
          <div class="color-preview-box" :style="`background:${gradient}`" @close="()=>{
            this.show = false
          }"></div>
        </div>
      </div>
    </div>
    <Dialog title="复制样式" v-if="show"  :show="show" @close="()=>{
      this.show = false
    }" >
      {{ gradient }}
    </Dialog>
    <Footer></Footer>
  </div>
</template>
<script>
import Header from '@/components/header.vue'
import Footer from '@/components/footer.vue'
import GradientMakerSlider from './components/gradientMakerSlider.vue';
import Dialog from './components/dialog.vue';
export default {
  name: 'Index',
  components: {
    Header,
    Footer,
    GradientMakerSlider,
    Dialog
  },
  data() {
    return {
      show:false,
      gradient: '',
      color1Data: {
        color: "#95ECB0",
        postion: 0,
        rotaion: 90,
        type: "linear",
      },
      color2Data: {
        color: "#F3F98A",
        postion: 100,
        rotaion: 90,
        type: "linear",
      },
      currColor: "color1"
    };
  },
  methods: {
    returnGradient(color) {
      this.gradient = color
    },
    getClickColor(color) {
      this.currColor = color
    },
    // 随机生成颜色
    randomFun(){
      const color1 = `#${Math.floor(Math.random() * 0xffffff).toString(16)}`;
      const color2 = `#${Math.floor(Math.random() * 0xffffff).toString(16)}`;
      this.color1Data.color = color1
      this.color2Data.color = color2
    }
  },
  mounted() {

  },
}
</script>
<style lang="less">
#app {
  width: 100%;
  height: 100%;
  background-color: #fff;
  font-family: "Inter", sans-serif;
  -webkit-font-smoothing: antialiased;

  .content {
    min-width: 1024px;
    margin: 0 auto;
    height: 100%;
    background-color: #fff;
    padding: 100px 0;

    .content-title {
      color: #000;
      text-align: center;
      font-weight: 700;
      font-size: 28px;
      letter-spacing: 0px;
    }

    .content-desc {
      margin-top: 20px;
      color: #7d7c83;
      text-align: center;
      font-weight: 400;
      font-size: 20px;
      letter-spacing: 0px;
    }

    .console {
      display: flex;
      padding-top: 100px;
      width: 1024px;
      margin: 0 auto;
      justify-content: center;
      align-items: center;


      .console-seting {
        margin: 0 20px;
        border: #E6E6E6 1px solid;
        border-radius: 10px;
        padding: 40px 10px;

        .setColor {
          display: flex;
          justify-content: space-around;
          text-align: center;
        }

        .color-info {
          display: flex;
          justify-content: space-around;
          text-align: center;
          flex-wrap: wrap;

          // 每行2个
          .color-info-item {
            width: 50%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            

            .color-input {
              width: 200px;
              height: 30px;
              border: #E6E6E6 1px solid;
              border-radius: 5px;
              padding: 0 10px;
            }
            
            .color-eye {
              width: 60px;
              height: 30px;
              border: #E6E6E6 1px solid;
              border-radius: 5px;
              padding: 0 10px;
              background:  no-repeat right center;
              background-size: 20px;
            }
          }
        }
      }

      .color-preview {
        margin: 0 20px;

        .color-preview-box {
          width: 300px;
          height: 300px;
          background-color: red;
        }
      }
    }
  }
  .BtnGroup{
    display: flex;
    justify-content: right;
    
    margin: 20px 0 0 0;

    .btn-random{
      width: 100px;
      height: 40px;
      background-color: #FFF;
      color: #000;
      border-radius: 5px;
      display: flex;
      justify-content: center;
      align-items: center;
      cursor: pointer;
      margin-right: 20px;
      border: 1px solid #e6e6e6 ;
    }
    .btn-Copy{
      width: 100px;
      height: 40px;
      background-color: #0066ff;
      color: #fff;
      border-radius: 5px;
      display: flex;
      justify-content: center;
      align-items: center;
      cursor: pointer;
    }
  }
}
</style>