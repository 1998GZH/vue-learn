<template>
  <g-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px">
    <g-item label="用户名" prop="username">
      <g-input type="text" v-model="ruleForm.username" />
    </g-item>
    <g-item label="密码" prop="password">
      <g-input type="text" v-model="ruleForm.password" />
    </g-item>
    <g-item>
      <el-button type="primary" @click="submitForm('ruleForm')">提交</el-button>
      <el-button @click="resetForm('ruleForm')">重置</el-button>
    </g-item>
  </g-form>
</template>

<script>
import GForm from "../components/ggform/GForm";
import GItem from "../components/ggform/GItem";
import GInput from "../components/ggform/GInput";

export default {
  components: {
    GForm,
    GItem,
    GInput
  },
  data() {
    let checkUsername = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("用户名不能为空!"));
      } else if (typeof value === "string" && value.length < 6) {
        callback(new Error("用户名不能小于6位!"));
      } else {
        callback();
      }
    }
    let checkPassword = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("密码不能为空!"))
      } else if (typeof value === "string" && value.length < 6) {
        callback(new Error("密码不能小于6位!"));
      } else {
        callback();
      }
    }
    return {
      ruleForm: {
        username: "",
        password: ""
      },
      rules: {
        username: [{validator: checkUsername, trigger: "blur"}],
        password: [{validator: checkPassword, trigger: "blur"}]
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  }
};
</script>

<style>
</style>