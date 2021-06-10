<template>
    <form @submit="addTask" class="d-flex justify-content-between align-items-end mb-4">
        <div class="form-group">
            <label>Task</label>
            <input required type="text" name="text" class="form-control" placeholder="Add Task" v-model="text">
        </div>
        <div class="form-group">
            <label>Day & Time</label>
            <input type="text" name="day" class="form-control" placeholder="Add Day & Time" v-model="day">
        </div>
        <div class="form-check">
            <input type="checkbox" class="form-check-input" name="reminder" v-model="reminder"> 
            <label>Remind me</label>
        </div>
        <button type="submit" class="btn btn-success">Save Task</button>
    </form>
</template>
<script>
export default{
    name:"AddTask",
    data(){
        return {
            text: '',
            day: '',
            reminder: false
        }
    },
    methods:{
        addTask(e){
            e.preventDefault()
            const new_task = {
                // id: Math.floor(Math.random()*100000),
                text: this.text,
                day: this.day,
                reminder: this.reminder
            }
            this.text = ''
            this.day = ''
            this.reminder = false

            console.log(new_task)
            this.$emit('add-task',new_task)
        }
    }
}
</script>