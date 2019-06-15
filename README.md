# modal2vue

> A simple modal component based on Vue, service to Vue project

[HomePage](https://modal2vue-kqxajeikuv.now.sh)

## 安装

npm i modal2vue

## 全局使用

```javascript
import Modal2vue from "modal2vue";
Vue.use(Modal2vue);
```

## 具体编码

```javascript
<template>
  <button @click="openModal" class="info-btn">Info</button>
  <modal2vue />
</template>

export default {
  methods: {
  openModal() {
      let config = {
        title: "title",//标题
        message: "message is here to show",//内容
        cancelBtnText: "cancel",//取消按钮文本
        confirmBtnText: "confirm",//确定按钮文本
        onCancel: null,//取消按钮点击事件
        onConfirm: null,//确定按钮点击事件
        showCancel: true,//是否展示取消按钮
        showClose: true,//是否展示关闭小叉号
        showMask: true,//是否展示蒙层
        maskClosable: true,//是否可以通过点击蒙层关闭modal
        afterClose: null,//关闭之后的回调
        type: 'info',//弹出类型 "info"|"warning"|"error"|"success"
        smooth: true,//是否使用平滑进出场动画
      }
      $modal2vue.onopen(config);
    }
  }
}
```

## api
```javascript
  $modal2vue.onopen(config);//关闭modal

  $modal2vue.onclose();//关闭modal

  $modal2vue.onconfirm();//调用确定按钮的点击事件

  $modal2vue.oncancel();//调用取消按钮的点击事件
```
