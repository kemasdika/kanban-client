<template>
    <div class="col-12 com-sm-6 col-md-3">
        <div class="form-container">

        <form @submit.prevent="onRegister">
            <p class="logo text-center">kanban</p>
            <h4 class="text-center">Register</h4>
            <hr>
            <div class="form-group">
                <label for="">Email address</label>
                <input type="text"
                  placeholder="e.g. email@gmail.com"
                  class="form-control"
                  v-model="email"
                  required>
            </div>
            <div class="form-group">
                <label for="">Password</label>
                <input type="password"
                  placeholder="*******"
                  class="form-control"
                  v-model="password"
                  required>
            </div>
            <button type="submit" class="btn btn-warning form-control">Submit</button>
        </form>
            <p class="pt-2 text-center">Already have an account <a href="" @click.prevent="toLogin">login</a></p>
            <p class="p-0 m-0 text-center fs-1" style="font-size: 15px;">--- or login with ---</p>
                <p class="text-center pt-2 pb-0 mb-0">
                    <button v-google-signin-button= 'clientId' class="google-signin-button btn btn-light"><img src="https://img.icons8.com/color/16/000000/google-logo.png" width="20px"> google</button>
                </p>            
        </div>
    </div>
</template>

<script>
import axios from "axios"
import GoogleSignInButton from 'vue-google-signin-button-directive'
export default {
    name:"Register",
    props: ["checkAcc",'fetchTask','changeStatus'],
    data() {
        return {
            email: "",
            password: "",
            url: "http://localhost:3000",
            clientId: '814646317355-7kb2krb937suas00beohh2idv5pmkbum.apps.googleusercontent.com'
        }
    },
    methods: {
        toLogin() {
            this.checkAcc(true)
        },
        onRegister() {
            console.log(this.email,this.password)
            axios({
                method: 'POST',
                url: `${this.url}/users/register`,
                data:{
                    email: this.email,
                    password: this.password,
                }
            })
            .then((response) => {
                this.checkAcc(true)
                console.log('register berhasil')
            })
            .catch(err => {
                console.log(err)
            })
        },
        OnGoogleAuthSuccess (idToken) {
			// console.log(idToken)
			axios({
                method: 'POST',
                url: `${this.url}/users/loginGoogle`,
                data: {
                    googleToken: idToken
                }
            })
            .then((response) => {
                    localStorage.setItem('access_token', response.data.access_token)
                    this.changeStatus(true)
                    this.fetchTask()
                        // console.log(response)
            })
            .catch((err) => {
                console.log(err)
            })
        },
        OnGoogleAuthFail (error) {
			console.log(error)
        }
    }
}
</script>

<style>

</style>