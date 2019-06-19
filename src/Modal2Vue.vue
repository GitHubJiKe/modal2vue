<template>
  <transition :name="transitionName">
    <div class="modal-container" v-if="open">
      <div class="modal-content" :style="{width: modalContentWidth}">
        <span class="iconfont iconclose close" v-if="showClose" @click="onclose"></span>
        <span :class="modalIconClass"></span>
        <p class="modal-title">{{title}}</p>
        <div class="modal-message">{{message}}</div>
        <div class="modal-btns">
          <button v-if="showCancel" class="modal-btn cancel" @click="oncancel">{{cancelBtnText}}</button>
          <button class="modal-btn confirm" @click="onconfirm">{{confirmBtnText}}</button>
        </div>
      </div>
      <div class="modal-mask" v-if="showMask && maskClosable" @click="onclose"></div>
      <div class="modal-mask" v-else-if="showMask"></div>
    </div>
  </transition>
</template>

<script>

export default {
  name: 'modal2vue',
  data() {
    return {
      title: "title",
      message: "message is here to show",
      cancelBtnText: "cancel",
      confirmBtnText: "confirm",
      onCancel: null,
      onConfirm: null,
      showCancel: true,
      showClose: true,
      open: false,
      showMask: true,
      maskClosable: true,
      afterClose: null,
      type: 'info',
      smooth: true
    }
  },
  mounted() {
    window.$modal2vue = this;
  },
  beforeDestroy() {
    window.$modal2vue = null;
  },
  methods: {
    onopen(config = { type: "info" }) {
      if (!config) {
        return;
      }
      this.$data.open = true;
      Object.keys(config).forEach(k => this.$data[k] = config[k])
    },
    onclose() {
      this.open = false;
      this.afterClose && this.afterClose();
    },
    oncancel() {
      this.onCancel && this.onCancel();
      this.open = false;
    },
    onconfirm() {
      this.onConfirm && this.onConfirm();
      this.open = false;
    }
  },
  computed: {
    modalIconClass() {
      return `iconfont icon${this.type} modal-icon ${this.type}`;
    },
    transitionName() {
      return this.smooth ? "fade" : '';
    },
    modalContentWidth() {
      return window.outerWidth > 500 ? '30%' : '80%';
    }
  }
}
</script>

<style>
@import url(//at.alicdn.com/t/font_1244083_ktvsin0l2zf.css);
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.4s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
.modal-container {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: transparent;
  display: flex;
  text-align: center;
  align-items: center;
  justify-content: center;
  z-index: 9999;
  user-select: none;
}
.modal-content {
  height: 300px;
  background-color: white;
  border: 1px solid #bfbfbf;
  border-radius: 10px;
  display: inline-block;
  z-index: inherit;
  padding: 10px;
}
.modal-btns {
  margin-top: 100px;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.modal-btn {
  width: 80px;
  height: 40px;
  border: none;
  outline: none;
  border-radius: 5px;
  font-size: 14pt;
  -webkit-transition-duration: 0.4s;
  transition-duration: 0.4s;
  cursor: pointer;
}
.close {
  position: absolute;
  right: 10%;
  cursor: pointer;
}
.modal-title {
  text-align: center;
  font-size: 30pt;
  padding: 0;
  margin: 0;
}
.modal-message {
  position: relative;
  top: 35px;
  text-align: center;
  font-size: 20pt;
  padding: 0;
  margin: 0;
}
.modal-mask {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: black;
  opacity: 0.8;
}
.modal-icon {
  font-size: 25pt;
}

.confirm {
  background-color: #1890ff;
  color: white;
}
.confirm:hover {
  background-color: #40a9ff;
}
.cancel {
  background-color: #bfbfbf;
  color: black;
}
.cancel:hover {
  background-color: #d9d9d9;
}
.info {
  color: #1890ff;
}
.warning {
  color: #faad14;
}
.error {
  color: #f5222d;
}
.success {
  color: #52c41a;
}
</style>
