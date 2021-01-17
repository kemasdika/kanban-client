<template>
    <section>
        <div class="container p-0">
            <h1 class="h3 mb-3">Kanban Board</h1>
            <div class="d-flex flex-row">
               <CategoryList
               v-for="task in dataTask" :key="task.id" :task='task'
               @createNewTask = 'createTask'
               @deleteTask='deleteThisTask'
               @editForm ='editThisForm'
               :allData='dataTask'
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
        editThisForm(editTask){
            this.$emit('editForm',editTask)
        }
    }

}
</script>

<style>

</style>