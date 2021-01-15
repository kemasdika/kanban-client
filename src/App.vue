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
        @editTask= 'editThisTask'
        @deleteTask='deleteThisTask'
        ></KanbanBoard>
    </div>
</template>

<script>
import Navbar from "./components/Navbar"
import Auth from "./components/Auth"
import KanbanBoard from "./components/KanbanBoard"
import axios from 'axios'
export default {
    name: "App",
    data() {
        return {
         isLogin : false,
         hasAccount : false,
         pageName: 'Auth',
         url:'http://localhost:3000',
         tasks:[]
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
                this.fetchTask()
            })
            .catch((err) => {
                console.log(err)
            })
        },
        editThisTask(editTask) {
            // console.log(editTask, 'dari app')
            const id = editTask.editTaskId
            const title = editTask.editTitle
            const CategoryId = editTask.editCategory
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
            .then((response) => {
                this.fetchTask()
            })
            .catch((err) => {
                console.log(err)
            })
        },
        deleteThisTask(id) {
            if (result.isConfirmed) {
            axios({
                url: `${this.url}/tasks/${id}`,
                method: 'DELETE',
                headers: {
                access_token: localStorage.getItem('access_token')
                }
            })
            .then((data) => {
                this.fetchTask()
            })
            .catch((err) => {
                console.log(err)
            })
            }
        },
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