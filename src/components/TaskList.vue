<template>
  <div class="card mb-3 bg-light">
        <div class="card-body p-3">
            <div class="float-right mr-n2">   
            </div>
            <p>{{taskKecil.title}}</p>
            <TaskUpdateForm v-if="isUpdate" 
            :taskKecil='taskKecil' 
            :task='task'
            :editForm="editForm"
            @closeEditTaskForm='editStatusToTrue'
            @editTaskSubmit='editThisTask'
             ></TaskUpdateForm>
            <div class="text-right p-0 m-0">
                <button type="button" class="btn btn-default btn-sm" @click="changeToUpdateForm">
                    <span class="fa fa-edit"></span>
                </button>
                <button type="button" class="btn btn-default btn-sm" @click='deleteTask'>
                    <span class="fa fa-trash"></span>
                </button>
            </div>
        </div>
    </div>
</template>

<script>
import TaskUpdateForm from "./TaskUpdateForm"
export default {
    name: "TaskList",
    components: {
        TaskUpdateForm
    },
    props: ['taskKecil', 'task'],
    data(){
        return{
            isUpdate: false,
            editTitle: '',
            editCategory: '',
        }
    },
    methods:{
        deleteTask() {
            this.$emit('deleteTask', this.taskKecil.id)
        },
        changeToUpdateForm(){
            this.isUpdate = true
        },
        editStatusToTrue(id) {
            this.editForm = id
            this.isUpdate = !this.isUpdate
        },
        editThisTask(editTask) {
            this.$emit('editTask', editTask)
        },
    }

}
</script>

<style>

</style>