<template>
</template>

<script>
export default {
  name: "modal",
  props: {
    // 弹框类型:小small 中middle 大large 表单form
    modalType: {
      type: String,
      default: "form",
    },
    // 弹框标题
    title: String,
    //按钮类型: 1.确定按钮  2.取消按钮  3.确定取消
    btnType: String,
    sureText: {
      type: String,
      default: "确定",
    },
    cancelText: {
      tyoe: String,
      default: "取消",
    },
    showModal: Boolean,
  },
};
</script>

<style lang="scss">
@import "./../assets/scss/config.scss";
@import "./../assets/scss/mixin.scss";
@import "./../assets/scss/modal.scss";
</style>
