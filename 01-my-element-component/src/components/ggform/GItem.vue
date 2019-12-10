<template>
  <div class="g-item-wrap">
    <div class="g-item">
      <span class="label" :style="{'flex-basis': form.labelWidth}">{{label}}</span>
      <slot></slot>
    </div>
    <p class="info" :class="infoShow?'info-show':''">{{infoMessage}}</p>
  </div>
</template>

<script>
import Schema from "async-validator";
export default {
  inject: ["form"],
  props: {
    label: {
      type: String
    },
    prop: {
      type: String
    }
  },
  data() {
    return {
      infoShow: false,
      infoMessage: ""
    };
  },
  created() {
    this.$on("validate", this.validate);
  },
  mounted() {
    // 告诉需要校验数据父组件自己已经挂载好了可以进行数据校验了
    if (this.prop) {
      this.$parent.$emit("childMounted", this);
    }
  },
  methods: {
    validate() {
      let descriptor = {
        [this.prop]: this.form.rules[this.prop]
      };
      let validator = new Schema(descriptor);
      let validateData = { [this.prop]: this.form.model[this.prop] };
      return new Promise(resolve => {
        validator.validate(validateData, errors => {
          if (errors) {
            let message = errors[0].message;
            this.infoShow = true;
            this.infoMessage = message;
            return resolve(false);
          } else {
            this.infoMessage = "";
            this.infoShow = false;
            return resolve(true);
          }
        });
      });
    },
    reset() {
      this.infoShow = false;
      this.infoMessage = "";
    }
  }
};
</script>

<style>
.g-item-wrap {
  margin-bottom: 10px;
}
.label {
  flex-basis: 100px;
  text-align: right;
  padding-right: 10px;
  font-size: 14px;
  color: #666;
}
.g-item {
  display: flex;
  justify-content: center;
  align-items: center;
}
.info {
  height: 12px;
  text-align: left;
  text-indent: 105px;
  font-size: 12px;
  color: #e23e3e;
  margin: 5px 0;
  opacity: 0;
  transition: opacity 0.5s linear;
}
.info-show {
  opacity: 1;
}
</style>