<template>
  <section id="auth" class="conteiner-fluid bg">
    <div class="row justify-content-center" id="form-login">
        <LoginForm
       v-if= "hasAccount"
       :changeStatus= "changeStatus"
       :checkAcc= "checkAcc"
       :fetchTask= "fetchTask"
        ></LoginForm>
        <Register
        v-if= "!hasAccount"
       :hasAccount= "hasAccount"
       :checkAcc= "checkAcc"
       :fetchTask= "fetchTask"
       :changeStatus= "changeStatus"
        ></Register>
    </div>
  </section>
</template>

<script>
import LoginForm from './LoginForm';
import Register from './Register'

export default {
    name:"Auth",
    props:['hasAccount','changeStatus','checkAcc','fetchTask'],
    components: {
        LoginForm,
        Register
    },
    data() {
      return {
        isShow: true
      }
    }
}
</script>

<style>

</style>