<template>
  <div class="wrap">
    <slot></slot>
  </div>
</template>

<script>
export default {
  provide() {
    return {
      gForm: this
    }
  },
  props: {
    "model": Object,
    "rules": Object,
    "label-width": String,
  },
  data() {
    return {
      isValidate: true
    }
  },
  methods: {
    validate() {
      this.isValidate = !this.isValidate;
    }
  }
}
</script>

<style scoped>

</style>