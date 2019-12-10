<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <Form/>
    <hr>
    <g-test-form/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Form from '../components/Form.vue'
import GTestForm from "../components/TestForm2"

export default {
  name: 'home',
  components: {
    HelloWorld,
    Form,
    GTestForm
  }
}
</script>
