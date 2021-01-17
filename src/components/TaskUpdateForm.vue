<template>
<div>
    <form @submit="editForm">
        <input type="text" class="form-control" v-model="editTask.title">
        <select id="inputState" class="form-control mt-2" v-model="editTask.category">
            <option v-for="data in allData" :key="data.id" 
            :value="data.id" 
            :data='data'> {{ data.name }}</option>
        </select>
            <button class="btn btn-warning form-control mt-2" type="submit">submit</button>
    </form>
</div>
</template>

<script>
export default {
    name: "TaskUpdateForm",
    props: ['taskKecil', 'task','allData'],
    data() {
        return{
            editTask: {
                title: this.taskKecil.title,
                id: this.taskKecil.id,
                category: this.task.id
            },
        }
    },
    methods:{
        editForm(){
            this.$emit('editForm',this.editTask)
            this.$emit('closeFormEdit',false)
        }
    }
}
</script>

<style>

</style>