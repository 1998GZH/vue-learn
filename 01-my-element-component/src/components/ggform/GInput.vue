<template>
  <input class="g-input" :type="type" :value="value" @input="inputHandler">
</template>

<script>
export default {
  inject: ["form"],
  props: {
    type: {
      type: String
    },
    value: {
      type: String
    }
  },
  methods: {
    inputHandler(e) {
      this.$emit("input", e.target.value);
      // 通知父组件进行数据校验
      this.$parent.$emit("validate");
    }
  }
}
</script>

<style>
.g-input {
  width: 100%;
  height: 35px;
  border: 1px solid #ddd;
  border-radius: 5px;
  text-indent: 0.5em;
  outline: none;
  transition: border-color 0.5s linear;
}
input.error{
  border-color: #ff0000cb;
}
.g-input:focus {
  border-color: rebeccapurple;
}
</style>