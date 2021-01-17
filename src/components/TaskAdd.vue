<template>
    <div class="card mb-3 bg-light">
        <TaskAddForm v-if="isAdd" :task='task' @createTask="addNewTask" @closeAddForm='closeAddForm'></TaskAddForm>        
        <a href="#" class="btn btn-warning btn-block" @click="changeToFormAdd">Add new</a>
    </div>
</template>

<script>
import TaskAddForm from "./TaskAddForm"
export default {
    name: "TaskAdd",
    components: {
        TaskAddForm
    },
    data() {
        return{
            isAdd:false
        }
    },
    methods:{
        changeToFormAdd() {
            this.isAdd = true
        },
        closeAddForm (v){
            this.isAdd = v
        },
        addNewTask(newTask) {
        this.$emit('createNewTask', newTask)
        },
    },
    props:['task']
}
</script>

<style>

</style>