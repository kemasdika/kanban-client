<template>
  <div class="kanban-app">
        <Navbar
        :changeStatus="changeIsLogin"
        :isLogin="isLogin"
        :checkAcc="checkAcc"
        :hasAccount="hasAccount"
        ></Navbar>
        <!-- login / register -->
        <Auth
        v-if= "!isLogin"
        :hasAccount= "hasAccount"
        :changeStatus= "changeIsLogin"
        :checkAcc= "checkAcc"
        :fetchTask= "fetchTask"
        ></Auth>
        <!-- kanban board -->
        <KanbanBoard
        v-if="isLogin"
        :dataTask= 'tasks'
        @createNewTask = 'createTask'
        @deleteTask='deleteThisTask'
        @editForm='editThisForm'
        ></KanbanBoard>
    </div>
</template>

<script>
import Navbar from "./components/Navbar"
import Auth from "./components/Auth"
import KanbanBoard from "./components/KanbanBoard"
import axios from 'axios'
import Swal from 'sweetalert2'
export default {
    name: "App",
    data() {
        return {
         isLogin : false,
         hasAccount : false,
         pageName: 'Auth',
         url:'https://kanbanku-c.herokuapp.com',
        //  url:'http://localhost:3000',
         tasks:[],
         email:''
        }
    },
    components:{
        Navbar,
        Auth,
        KanbanBoard
    },
    methods: {
        changeIsLogin(value) {
         this.isLogin = value;
        },
        checkAcc(value) {
         this.hasAccount = value;
        },
        fetchTask() {
            axios({
                url: `${this.url}/categories`,
                method: 'GET',
                headers: {
                access_token: localStorage.getItem('access_token')
                }
            })
            .then((response) => {
                // console.log(response.data)
                this.tasks = response.data
            })
            .catch((err) => {
                console.log(err)
            })
        },
        createTask(newTask) {
            axios({
                url: `${this.url}/tasks`,
                method: 'POST',
                data: {
                title: newTask.taskTitle,
                CategoryId: newTask.taskCategoryId
                },
                headers: {
                access_token: localStorage.getItem('access_token')
                }
            })
            .then((data) => {
                Swal.fire({
					icon: 'success',
					title: 'Nice !',
					text: 'Your new Task has been Created',
                })
                this.fetchTask()
            })
            .catch((err) => {
                Swal.fire({
					icon: 'error',
					title: 'Oops...',
					text: 'Something went wrong!',
                })
                console.log(err)
            })
        },
        deleteThisTask(id) {
        Swal.fire({
            title: 'Are you sure?',
            text: "You won't be able to revert this!",
            icon: 'warning',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, delete it!'
        }).then((result) => {
            if (result.isConfirmed) {
                axios({
                    url: `${this.url}/tasks/${id}`,
                    method: 'DELETE',
                    headers: {
                    access_token: localStorage.getItem('access_token')
                    }
                })
                .then((data) => {
                    Swal.fire({
                        icon: 'success',
                        title: 'Okay..',
                        text: 'Your task has been Deleted',
                    })
                    this.fetchTask()
                })
                .catch((err) => {
                    console.log(err)
                    Swal.fire({
                        icon: 'error',
                        title: 'Oops...',
                        text: 'Are you sure this is your task?',
                    })
                })
            }
        })
        },
        editThisForm(editTask){
            const id = editTask.id
            const title = editTask.title
            const CategoryId = editTask.category
              axios({
                url: `${this.url}/tasks/${id}`,
                method: 'PUT',
                headers: {
                    access_token: localStorage.getItem('access_token')
                },
                data: {
                    title,
                    CategoryId
                }
            })
            .then((data) => {
                Swal.fire({
					icon: 'success',
					title: 'Nicee!',
					text: 'Your task has been Edited',
                })
                this.fetchTask()
            })
            .catch((err) => {
                console.log(err)
                Swal.fire({
					icon: 'error',
					title: 'Oops...',
					text: 'Are you sure this is your task?',
                })
            })
        }
    },
    created() {
        if (localStorage.getItem("access_token")) {
        this.isLogin = true;
        this.fetchTask()
        } else {
        this.isLogin = false;
        }
    },
}
</script>
<style>

</style>