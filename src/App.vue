<template>
  <div id="app">
    <!-- <cart></cart> -->
    <div id="tabber">

      <router-link to="/home">首页</router-link>
      <router-link to="/fenlei">分类</router-link>
      <router-link to="/vip">会员</router-link>
      <router-link to="/cart">购物车</router-link>
      <router-link to="/mine">我的</router-link>

    </div>
    <transition name="fade" mode='out-in'>
      <router-view></router-view>
    </transition>
  </div>
</template>

<script>
// import Cart from './cart/cart'
// import GoodDetail from './components/goodDetil'

export default {
  name: 'app',
  data() {
    return {
      name: ""
    }
  },
  components: {
    // Cart
  },
  computed: {

    direction() {
      const viewDir = this.$store.state.viewDirection
      let tranName = ''
      if (viewDir === 'left') {
        tranName = 'view-out'
      } else if (viewDir === 'right') {
        tranName = 'view-in'
      } else {
        tranName = 'fade'
      }

      return tranName
    },
  },
}
</script>

<style type="text/css">
.fade-enter-active,
.fade-leave-active {
  transition: all .2s ease;
}

.fade-enter,
.fade-leave-active {
  opacity: 0;
}

.view-in-enter-active,
.view-out-leave-active {
  position: absolute;
  top: 0;
  width: 100%;
  /* padding-top: px2rem($titbarHeight); */
  -webkit-animation-duration: .3s;
  animation-duration: .3s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}

.view-in-enter-active {
  -webkit-animation-name: inRight;
  animation-name: inRight;
}

.view-out-leave-active {
  -webkit-animation-name: outLeft;
  animation-name: outLeft;
}




/* 另一种动画 */


/* .bounce-enter-active {
  animation: bounce-in .5s;
}

.bounce-leave-active {
  animation: bounce-in .5s reverse;
}

@keyframes bounce-in {
  0% {
    transform: translate3d(100%, 0, 0);
    /* translate3d(-100%, 0, 0); */


/* } */


/* 50% {
    transform: scale(1.5);
  } */
/* 100% {
  transform: translate3d(0, 0, 0);
} */



/* } */
#tabber {
  width: 100%;
  height: 1.25rem;
  display: flex;
  z-index: 50;
  justify-content: space-around;
  align-items: center;
  /*font-size: 16px;*/
  background: #fff;
  position: fixed;
  bottom: 0;
  left: 0;
}

#tabber a {
  /*flex-direction:column;*/
  font-size: 0.35rem;
  line-height: 1.5rem;
  color: #828282;
}









/*路由跳转前给每个a标签加一个灰色的背景图，在点击路由跳转时，给a标签添加另外一个背景图
    需要在选中元素后加.router-link-active即可*/
#tabber a:nth-of-type(1) {
  background: url(./assets/btm-bar-sprt.png) no-repeat;
  display: block;
  width: 0.75rem;
  height: 0.75rem;
  background-size: 6.25rem;
  background-position: 0rem -0.1rem;
}

#tabber a:nth-of-type(1).router-link-active {
  background: url(./assets/btm-bar-sprt.png) no-repeat;
  display: block;
  width: 0.75rem;
  height: 0.75rem;
  color: #FF8D55;
  background-size: 6.25rem;
  background-position: 0rem -1.375rem;
  color: #FF8D55;
}

#tabber a:nth-of-type(2) {
  background: url(./assets/btm-bar-sprt.png) no-repeat;
  display: block;
  width: 0.75rem;
  height: 0.75rem;
  background-size: 6.25rem;
  background-position: -1.275rem -0.1rem;
}

#tabber a:nth-of-type(2).router-link-active {
  background: url(./assets/btm-bar-sprt.png) no-repeat;
  display: block;
  width: 0.75rem;
  height: 0.75rem;
  color: #FF8D55;
  background-size: 6.25rem;
  background-position: -1.275rem -1.325rem;
  color: #FF8D55;
}

#tabber a:nth-of-type(3) {
  background: url(./assets/btm-bar-sprt.png) no-repeat;
  display: block;
  width: 0.75rem;
  height: 0.75rem;
  background-size: 6.25rem;
  background-position: -2.575rem -0.125rem;
}

#tabber a:nth-of-type(3).router-link-active {
  background: url(./assets/btm-bar-sprt.png) no-repeat;
  display: block;
  width: 0.75rem;
  height: 0.75rem;
  color: #FF8D55;
  background-size: 6.25rem;
  background-position: -2.575rem -1.4rem;
  color: #FF8D55;
}

#tabber a:nth-of-type(4) {
  background: url(./assets/btm-bar-sprt.png) no-repeat;
  display: block;
  width: 0.75rem;
  height: 0.75rem;
  background-size: 6.25rem;
  background-position: -3.825rem -0.1rem;
}

#tabber a:nth-of-type(4).router-link-active {
  background: url(./assets/btm-bar-sprt.png) no-repeat;
  display: block;
  width: 0.75rem;
  height: 0.75rem;
  color: #FF8D55;
  background-size: 6.25rem;
  background-position: -3.8rem -1.375rem;
  color: #FF8D55;
}

#tabber a:nth-of-type(5) {
  background: url(./assets/btm-bar-sprt.png) no-repeat;
  display: block;
  width: 0.75rem;
  height: 0.75rem;
  background-size: 6.25rem;
  background-position: -5.05rem -0.1rem;
}

#tabber a:nth-of-type(5).router-link-active {
  background: url(./assets/btm-bar-sprt.png) no-repeat;
  display: block;
  width: 0.75rem;
  height: 0.75rem;
  color: #FF8D55;
  background-size: 6.25rem;
  background-position: -5.075rem -1.375rem;
  color: #FF8D55;
}

#tabber div {
  width: 20%;
  text-align: center;
}
</style>
