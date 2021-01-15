<template>
  <nav class="navbar navbar-expand-sm bg-light navbar-light fixed-top">
            <div class="container">
                <a class="navbar-brand logo" href="#">kanban</a>
                <ul class="navbar-nav"> 
                    <li class="nav-item dropdown"  v-if="isLogin">
                        <a class="nav-link dropdown-toggle" href="#" id="navbardrop" data-toggle="dropdown">
                            hallo
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
            localStorage.clear()
            this.changeStatus(false);
        }
    }
}
</script>

<style>

</style>