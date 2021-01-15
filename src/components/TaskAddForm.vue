<template>
  <div class="card-body p-3">
            <div class="float-right mr-n2">   
            </div>
            <form >
                <input type="text" v-model= "newTask.taskTitle" placeholder="new task" class="form-control" required>
                <button class="btn btn-warning form-control mt-2" type="submit" @click.prevent="createTask">submit</button>
            </form>
        </div>
</template>

<script>
export default {
    name: "TaskAddForm",
    data(){
        return{
            newTask: {
                taskTitle: '',
                taskCategoryId: this.task.id
            }
        }
    },
    props:['task'],
    methods:{
        createTask() {
                this.$emit('createTask', this.newTask)
                this.$emit('closeAddForm')
        }
    }
}
</script>

<style>

</style>