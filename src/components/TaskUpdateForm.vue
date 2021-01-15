<template>
<div>
    <form action="">
        <input type="text" placeholder="update task" class="form-control" v-model="editTask.editTitle">
        <select id="inputState" class="form-control mt-2" v-model="editTask.editCategory">
            <option selected>Choose...</option>
            <option :selected="task.name === 'Back-log'" 
            >Back-Log</option>
            <option :selected="task.name === 'Todo'">Todo</option>
            <option :selected="task.name === 'Ongoing'">Ongoing</option>
            <option :selected="task.name === 'Done'">Done</option>
            </select>
            <button class="btn btn-warning form-control mt-2" type="submit" @click.prevent="editTaskSubmit&&closeEditTaskForm">submit</button>
    </form>
</div>
</template>

<script>
export default {
    name: "TaskUpdateForm",
    props:['task','taskKecil'],
    data() {
        return {
            editTask: {
                editTitle: this.taskKecil.title,
                editCategory: this.task.id,
                editTaskId: this.taskKecil.id
            }
        }
    },
    methods: {
        closeEditTaskForm() {
			this.$emit('closeEditTaskForm')
		},
		editTaskSubmit() {
			this.$emit('editTaskSubmit', this.editTask)
			this.closeEditTaskForm()
		}
	},
}
</script>

<style>

</style>