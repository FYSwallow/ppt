<template>
  <div class="container clearfix">
    <aside class="container_left" ref="aside">
      <ul>
        <li v-for="(item, index) in data" :key="index" @click.capture="choose(index)" :class="{active: selected === index}">
          <v-common :msg="item"></v-common>
        </li>
      </ul>
    </aside>
    <section class="container_right">
      <div class="content">
        <v-common :msg="data[selected]"></v-common>
      </div>
      <div class="scale"  @mouseover="enter" @mouseout="out">
        <span class="left" v-if="selected !== 0" @click="prev" :style="{display: show}" >上一页</span>
        <span class="right" v-if="selected !== data.length-1" @click="next" :style="{display: show}" >下一页</span>
      </div> 
      <div class="fullScreen" @click="toggleFullScreen">
        <span v-show="!fullscreen">全屏</span>
        <span v-show="fullscreen">取消全屏</span>
      </div>
      <div class="description">鼠标移动到页脚,点击切换当前页</div>
    </section>
  </div>
</template>

<script>
import data from '@/assets/json/data.json'
import Common from '@/components/common'
import { setTimeout } from 'timers';

export default {
 
  data() {
      return{
          data: '',
          selected: 0,
          show: 'none',
          fullscreen: false
      }
  },
  created() {
      this.data = data.content
  },
  methods: {
    // 根据nav切换内容和样式
    choose(index){
      this.selected = index
    },
    // 鼠标进入时显示跳转按钮
    enter() {
      this.show = 'block' 
    },
    out() {
      this.show = 'none' 
    },
    // 跳转上一页
    prev() {
      this.selected --
    },
    next() {
      this.selected ++
    },
    // 全屏事件
    toggleFullScreen() {
        let element = document.documentElement;
        if (this.fullscreen) {
            if (document.exitFullscreen) {
                document.exitFullscreen();
            } else if (document.webkitCancelFullScreen) {
                document.webkitCancelFullScreen();
            } else if (document.mozCancelFullScreen) {
                document.mozCancelFullScreen();
            } else if (document.msExitFullscreen) {
                document.msExitFullscreen();
            }
            this.$refs.aside.style.display = 'block'
        } else {
            if (element.requestFullscreen) {
                element.requestFullscreen();
            } else if (element.webkitRequestFullScreen) {
                element.webkitRequestFullScreen();
            } else if (element.mozRequestFullScreen) {
                element.mozRequestFullScreen();
            } else if (element.msRequestFullscreen) {
                // IE11
                element.msRequestFullscreen();
            }
            this.$refs.aside.style.display = 'none'
        }
        this.fullscreen = !this.fullscreen;
    }
  },
   components:{
    'v-common': Common
  }
}
</script>

<style lang="scss">
@import './assets/style/base.css';
.container {
    width: 100%;
    height: 100%;
    display: flex;
    .container_left {
      width: 200px;
      height: 100%;
      margin: 5px;
      overflow: hidden;
      float: left;
      ul {
        width: 220px;
        height: 100%;
        overflow: auto;
        li {
            height: 200px;
            border: 3px solid #ccc;
            margin: 5px;
            overflow: hidden;
            &:hover {
                border-color: green; 
            }
            
        }
        .active{
            border-color: green; 
        }
      }
    }
    .container_right {
      flex: 1;
      .content{
        width: 100%;
        height:100%;
        align-items: center;
        justify-content: center;
        div {
          width: 100%;
          height: 100%;
          background-size: 100% 100%;
        }
        img {
          width: 100%;
        }
      }  
      .scale {
        width: 100%;
        height:100px;
        position: fixed;
        bottom: 0px;
        font-size: 30px;
        span {
          position: absolute;
          &.left {
            left: 100px;
          }
          &.right {
            right: 300px;
          }
        } 
      }
      .fullScreen {
        width: 100px;
        height: 50px;
        position: fixed;
        top: 5px;
        right: 20px;
        text-align: center;
        font-size: 20px;
        color: red;
      }
      .description {
        position: absolute;
        top: 50%;
        left: 50%;
        animation: fade 5s linear;
        opacity: 0;
        font-size: 30px;
      }
      @keyframes fade {
        0% {
          opacity: 1;
          transform: translate(0, 0);
          font-size: 30px;
        }
        50% {
          opacity: 1;
          transform: translate(0, 0);
          font-size: 30px;
        }
        75% {
          opacity: 0.5;
          transform: translate(100px, 100px);
          font-size: 20px;
        }
        100% {
          opacity: 0;
          transform: translate(200px, 200px);
          font-size: 12px;
        }
      }
    }
}

</style>