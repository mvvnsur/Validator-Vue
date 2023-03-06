<template>
  <form id="app" class="sign-up my-5" @submit.prevent="checkForm">
    <div class="form-group my-4">
      <label for="login">Login:</label>
      <input 
      id="login"
      v-model.trim="form.login"
      class="form-control"
      :class="v$.form.login.$error ? 'is-invalid' : ''"
      >
      <p class="invalid-feedback">
        Essential row
      </p>
    </div>
    <div class="form-group my-4">
      <label for="login">Email:</label>
      <input 
      id="email"
      v-model.trim="form.email"
      class="form-control"
      :class="v$.form.email.$error ? 'is-invalid' : ''"
      >
      <p class="invalid-feedback">
        Email is incorrect
      </p>
    </div>
    <div class="form-group my-4">
      <label for="login">Password</label>
      <input 
      id="password"
      v-model.trim="form.password"
      class="form-control"
      :class="v$.form.password.$error ? 'is-invalid' : ''"
      >
      <p v-if="v$.form.password.$dirty && !v$.form.password.required" class="invalid-feedback">
        Essential Row
      </p>
      <p class="invalid-feedback">
        Password is incorrect
      </p>
    </div>
    <button type="submit" class="btn btn-light my-3">Send</button>
  </form>
</template>

<script>
import { useVuelidate } from '@vuelidate/core'
import { required, email, minLength } from '@vuelidate/validators'


export default {
  name: 'App',
  setup () {
    return { v$: useVuelidate() }
  },
  data() {
    return{
      form:{
        login: '',
        email: '',
        password: '',
      }
    }
  },
  validations() {
    return{
      form:{
        login: { required, minLength:minLength(8)},
        email: { required, email },
        password: { required, minLength:minLength(8) }
      }
    }
  },
  methods: {
    checkForm(){
      this.v$.form.$touch()
      if (!this.v$.form.$error){
        console.log('Validation was successful')
      }
    }
  }
}
</script>

<style>
  .sign-up{
    width: 400px;
    height: auto;
    margin: auto;
    background-color: #415380;
    border-radius: 10px;
    padding: 40px;
  }
  .form-group{
    text-align: left;
    color: white;
    font-size: 20px;
  }
  .btn{
    width: 200px;
    height: 50px;
  }
  p{
    color: red;
    font-size: 20px;
  }
</style>