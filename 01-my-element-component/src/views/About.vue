<template>
  <div class="about">
    <h1 @[event]="handle">this is about page!</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      event: "click"
    }
  },
  methods: {
    handle() {
      alert("xxx");
    }
  }
}
</script>

<style>

</style>