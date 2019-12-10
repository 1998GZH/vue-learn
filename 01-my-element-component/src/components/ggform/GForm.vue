<template>
  <div class="form-wrap">
    <slot></slot>
  </div>
</template>

<script>
export default {
  provide() {
    return {
      form: this
    };
  },
  props: {
    model: {
      type: Object,
      required: true
    },
    rules: {
      type: Object
    },
    labelWidth: {
      type: String
    }
  },
  created() {
    this.fields = [];
    this.$on("childMounted", child => {
      this.fields.push(child);
    });
  },
  methods: {
    async validate(callback) {
      let tasks = this.fields.map(item => item.validate());
      const result = await Promise.all(tasks);
      let ret = true;
      result.forEach(r => {
        if (!r) {
          ret = false;
        }
      });
      callback(ret);
    },
    resetFields() {
      this.fields.forEach(item => {
        item.form.model[item.prop] = "";
        item.reset();
      });
    }
  }
};
</script>

<style>
</style>