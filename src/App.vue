<template>
  <div class="app">
    <modal2-vue/>
    <button @click="openModal">open</button>
  </div>
</template>

<script>
import Modal2Vue from "./Modal2Vue.vue";
export default {
  name: 'App',
  components: {
    Modal2Vue
  },
  data() {
    return {
      title: "hello",
      message: "friends",
      cancelBtnText: "取消",
      confirmBtnText: "确定",
      onCancel: null,
      onConfirm: null,
      showCancel: true,
      showClose: true,
      open: true,
      showMask: true,
      maskClosable: false,
      afterClose: null,
      type: 'info',
      smooth: true
    }
  },
  methods: {
    openModal() {
      $modal2vue.onopen(this.$data);
    }
  }
}
</script>

<style>
.app {
  width: 100%;
  height: 500px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
