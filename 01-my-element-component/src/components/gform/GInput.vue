<template>
  <input :type="type" :value="value" @input="inputHandler" class="g-input" @blur="blurHandler"/>
</template>

<script>
export default {
  props: ["value", "type"],
  methods: {
    blurHandler() {
      this.$parent.$emit("validateData", this.value);
    },
    inputHandler(e) {
      let value = e.target.value;
      this.$emit("input", value);
    }
  },
  created() {
    this.$parent.$on("requestValidate", () => {
      this.blurHandler();
    });
  }
};
</script>

<style scoped>
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