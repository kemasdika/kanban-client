<template>
   <div class="col-12 col-lg-6 col-xl-3">
                    <div class="card card-border-primary">
                        <div class="card-header">
                        <h5 class="card-title">{{task.name}}</h5>
                    </div>
                    <div class="card-body p-3">
                        <TaskList
                        v-for="taskKecil in task.Tasks" :key="taskKecil.id" :taskKecil='taskKecil'
                         :dataTask='dataTask'
                         @editTask='editTaskSubmit'
                         :task='task'
                         @deleteTask='deleteThisTask'
                        ></TaskList>
                        <TaskAdd :task='task' @createNewTask="createTask"></TaskAdd>
                </div>
        </div>      
    </div>
</template>

<script>
import TaskList from "./TaskList"
import TaskAdd from "./TaskAdd"
export default {
    name: "CategoryList",
    components:{
        TaskList,
        TaskAdd
    },
    props: ['task'],
    data(){
        return {
            taskCategory: this.task.name,
         }
    },
    methods:{
        createTask(newTask) {
            this.$emit('createNewTask', newTask)
        },
        editTaskSubmit(editTask) {
            this.$emit('editThisTask', editTask)
        },
        deleteThisTask(id) {
            this.$emit('deleteTask', id)
        },
    }
}
</script>

<style>

</style>