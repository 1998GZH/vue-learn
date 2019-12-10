<template>
  <div class="wrap">
    <div class="gitem-wrap" :class="isShowErrorMessage?'error':''">
      <span class="label" :style="{'flex-basis': gForm.labelWidth}">{{ label }}</span>
      <slot></slot>
    </div>
    <p class="info" :class="isShowErrorMessage?'errorInfo':'successInfo'">{{errorMessage}}</p>
  </div>
</template>

<script>
export default {
  inject: ["gForm"],
  props: {
    label: String,
    prop: String
  },
  data() {
    return {
      errorMessage: "error",
      isShowErrorMessage: false
    };
  },
  created() {
    this.$on("validateData", value => {
      let rules = this.gForm.rules[this.prop];
      for (let rule of rules) {
        rule.validator(null, value, this.validatorFunc);
      }
    });
  },
  watch: {
    "gForm.isValidate": function() {
      this.$emit("requestValidate", "");
    }
  },
  methods: {
    validatorFunc(err) {
      if (err) {
        let message = err.message;
        this.errorMessage = message;
        this.isShowErrorMessage = true;
        return;
      } else {
        this.errorMessage = "";
        this.isShowErrorMessage = false;
      }
    }
  }
};
</script>

<style>
.wrap {
  margin-bottom: 5px;
}
.error > input.g-input {
  border-color: #ff0000cb !important;
}
.wrap .info {
  height: 12px;
  font-size: 12px;
  color: #ff0000cb;
  margin-top: 5px;
  text-align: left;
  text-indent: 105px;
  transition: opacity 0.5s linear;
}
.wrap .errorInfo {
  opacity: 1;
}
.wrap .successInfo {
  opacity: 0;
}
.gitem-wrap {
  display: flex;
  justify-content: center;
  align-items: center;
}
.gitem-wrap .label {
  flex-basis: 100px;
  text-align: right;
  padding-right: 10px;
}
</style>