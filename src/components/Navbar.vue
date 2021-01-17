<template>
  <nav class="navbar navbar-expand-sm bg-light navbar-light fixed-top">
            <div class="container">
                <a class="navbar-brand logo" href="#">kanban</a>
                <ul class="navbar-nav"> 
                    <li class="nav-item dropdown"  v-if="isLogin">
                        <a class="nav-link dropdown-toggle" href="#" id="navbardrop" data-toggle="dropdown">
                            hai
                        </a>
                        <div class="dropdown-menu">
                            <button class="btn text-danger"  @click.prevent="onSignOut">Logout</button>                                
                    </div>
                    </li>                        
                    <li class="nav-item dropdown"  v-if="!isLogin">
                        <a class="nav-link dropdown-toggle" href="#" id="navbardrop" data-toggle="dropdown">
                            Menu
                        </a>
                        <div class="dropdown-menu">
                            <a class="dropdown-item" href="#"  @click.prevent="toRegister">Register</a>
                            <a class="dropdown-item" href="#" @click.prevent="toLogin">Login</a>                 
                        </div>
                    </li>
                </ul>
            </div>
  </nav>
</template>

<script>
import Swal from 'sweetalert2'
export default {
    name: "Navbar",
    props: ["changeStatus", "isLogin", "hasAccount", "checkAcc"],
    methods: {
        toRegister() {
            this.checkAcc(false);
        },
        toLogin() {
            this.checkAcc(true);
        },  
        onSignOut(){
            Swal.fire({
				title: 'Are you sure?',
				text: "You can back any time to see your task",
				icon: 'warning',
				showCancelButton: true,
				confirmButtonColor: '#3085d6',
				cancelButtonColor: '#d33',
				confirmButtonText: "Yes, i'm leaving~"
			}).then((result) => {
				if (result.isConfirmed) {
                    localStorage.clear()
                    this.changeStatus(false);
					Swal.fire({
						icon: 'success',
						title: 'Good Bye',
						text: 'Thank you for your visit, have a nice day',
					})
				}
			})
        }
    }
}
</script>

<style>

</style>