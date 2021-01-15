<template>
    <section>
        <div class="container p-0">
            <h1 class="h3 mb-3">Kanban Board</h1>
            <div class="d-flex flex-row">
               <CategoryList
               v-for="task in dataTask" :key="task.id" :task='task'
               @createNewTask = 'createTask'
               @editTaskSubmit='editThisTask'
               :editForm="editForm"
               @deleteTask='deleteThisTask'
               ></CategoryList>
            </div>
        </div>
    </section>
</template>

<script>
import CategoryList from "./CategoryList"
export default {
    name: "KabanBoard",
    components:{
        CategoryList
    },
    data(){
        return{
            editForm:{}
        }
    },
    props: ['dataTask'],
    methods:{
        deleteThisTask(id) {
            this.$emit('deleteTask', id)
        },
        createTask(newTask) {
            this.$emit('createNewTask', newTask)
        },
         editThisTask(editTask) {
            this.$emit('editTask', editTask)
        },
        editStatusToTrue(id) {
            this.editForm = id
            this.editStatus = !this.editStatus
        },

    }

}
</script>

<style>

</style>