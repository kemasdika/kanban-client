<template>
    <div class="col-12 com-sm-6 col-md-3">
        <div class="form-container">
            <form  @submit.prevent="onLogin">
                <p class="logo text-center">kanban</p>
                <h4 class="text-center">Login</h4>
                <hr>
                <div class="form-group">
                    <label for="">Email address</label>
                    <input type="text"
                    placeholder="e.g. email@gmail.com"
                    class="form-control"
                    v-model="email"
                    >
                </div>
                <div class="form-group">
                    <label for="">Password</label>
                    <input type="password"
                    placeholder="*******"
                    class="form-control"
                    v-model="password"
                    >
                </div>
                    <button type="submit" class="btn btn-warning form-control">Submit</button>
            </form>
                <p class="pt-2 text-center">Don't have an account <a href="" @click.prevent="toRegister">register</a></p>
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
import Swal from 'sweetalert2'
export default {
    name: "LoginForm",
    props:["changeStatus","checkAcc","onFailure",'fetchTask'],
    data() {
        return {
            email: "",
            password: "",
            url: 'https://kanbanku-c.herokuapp.com',
            clientId: '814646317355-v8pgb06iql2klkvpvfj9n7cadj9pnpck.apps.googleusercontent.com'
        }
    },
    methods: {
        toRegister() {
            this.checkAcc(false)
        },
        onLogin() {
            axios({
                method: 'POST',
                url: `${this.url}/users/login`,
                data:{
                    email: this.email,
                    password: this.password
                },
            })
            .then(({data}) => {
                localStorage.setItem("access_token",data.access_token)
                Swal.fire({
					icon: 'success',
					title: `Hi ${this.email}`,
					text: 'Welcome to Kanban Apps ',
				})
                this.changeStatus(true)
                this.fetchTask()
            })
            .catch((err) => {
                console.log(err)
                Swal.fire({
					icon: 'error',
					title: 'Oops...',
					text: 'Something went wrong!',
				})
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
                    Swal.fire({
                        icon: 'success',
                        title: `Hi ${this.email_input}`,
                        text: 'Welcome to Kanban Apps ',
                    })
                    this.changeStatus(true)
                    this.fetchTask()
                        // console.log(response)
            })
            .catch((err) => {
                Swal.fire({
					icon: 'error',
					title: 'Oops...',
					text: 'Something went wrong, Check again your Google Account!',
				})
                console.log(err)
            })
        },
        OnGoogleAuthFail (error) {
            console.log(error)
            Swal.fire({
					icon: 'error',
					title: 'Oops...',
					text: 'Are You Sure with your Google Account?',
            })
        }
    },

}
</script>

<style>

</style>