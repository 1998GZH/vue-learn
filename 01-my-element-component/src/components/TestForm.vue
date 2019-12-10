<template>
  <GForm :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px">
    <GItem label="账号" prop="username">
      <GInput type="text" v-model="ruleForm.username" />
    </GItem>
    <GItem label="密码" prop="password">
      <GInput type="password" v-model="ruleForm.password" />
    </GItem>
    <GItem>
      <el-button type="primary" @click="submitForm('ruleForm')">提交</el-button>
      <el-button @click="resetForm('ruleForm')">重置</el-button>
    </GItem>
  </GForm>
</template>

<script>
import GForm from "../components/gform/GForm";
import GItem from "../components/gform/GItem";
import GInput from "../components/gform/GInput";

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
      } else if (value.length < 6) {
        callback(new Error("用户名不能小于6位!"));
      } else {
        callback();
      }
    }
    let checkPassword = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("密码不能为空!"))
      } else if (value.length < 6) {
        callback(new Error("密码不能小于6位!"));
      } else {
        callback();
      }
    }
    return {
      ruleForm: {
        username: '',
        password: '',
      },
      rules: {
        username: [{validator: checkUsername, trigger: "blur"}],
        password: [{validator: checkPassword, trigger: "blur"}]
      }
    }
  },
  methods: {
    resetForm() {
      alert("功能未实现!");
    },
    submitForm(form) {
      this.$refs[form].validate();
    }
  }
};
</script>

<style>
</style>