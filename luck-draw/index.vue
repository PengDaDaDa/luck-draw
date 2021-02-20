<template>
  <van-overlay :show="showPop" z-index="999">
    <transition name="bounce">
      <div v-show="showPop" class="wrapper">
        <div class="conent">
          <!-- <img src="@/assets/images/hongbao_out.png" />
          <div class="words">恭喜您获得: {{ info && info }}</div>
          <p v-if="percent" class="p">（您的语音识别率为：{{ percent }}%）</p> -->
          <draw :info="info" @close="close" />
        </div>
      </div>
    </transition>
  </van-overlay>
</template>
<script>
import draw from './index2'
export default {
  components: { draw },
  props: {
    show: Boolean,
    info: Object,
    percent: {
      type: Number,
      default: null
    }
  },
  data () {
    return {}
  },
  computed: {
    showPop: {
      get () {
        return this.show
      },
      set (val) {
        this.$emit('update:show', val)
      }
    }
  },
  methods: {
    close () {
      this.showPop = false
      this.$router.push({ path: '/' })
    }
  }
}
</script>
<style lang="scss" scoped>
.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  .conent {
    position: relative;
  }
  img {
    width: 60vw;
    margin: 0 auto;
  }
  .words {
    position: absolute;
    color: white;
    top: 80px;
    width: 50vw;
    left: 5vw;
    text-align: center;
    font-size: 26px;
  }
  .p {
    position: absolute;
    color: white;
    bottom: 10px;
    width: 50vw;
    left: 5vw;
    text-align: center;
    font-size: 16px;
    color: #fed170;
  }
  .close {
    position: absolute;
    width: 30px;
    height: 30px;
    top: -50px;
    right: -20px;
  }
}
.bounce-enter-active {
  animation: bounce-in 1s;
}
.bounce-leave-active {
  animation: bounce-in 1s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}
</style>
