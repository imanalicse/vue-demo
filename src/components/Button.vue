<template>
  <button @click="btnClick()" :style="{ background: backgroundColor }" class="btn"> {{text}}</button>
</template>

<script>

export default {
  name: 'Button',
  props: {
      text: String,
      backgroundColor : String
  },
  methods: {
    btnClick() {
        console.log("click");
        this.$emit('btn-click');
    }
  }
};
</script>

<style scoped>
    .btn {
        background: green;
    }
</style>