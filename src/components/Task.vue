<template>
    <div @dblclick="$emit('toggle-reminder',task.id)" :class="[task.reminder ? 'reminder' : '','task']">
        <h3 class="d-flex justify-content-between align-items-center">{{task.text}}
            <i @click="deleteTask(task.id)" class="fas fa-times" />
        </h3>
        <p>{{task.day}}</p>
    </div>
</template>

<script>
export default{
    name:"Task",
    props:{
        task: Object
    },
    methods:{
        deleteTask(id){
            this.$emit('delete-task',id)
        }
    },
    emits: ['toggle-reminder']
}
</script>

<style scoped>
.task {
    background-color: #ececec;
    padding: 0.5rem 1rem;
    margin-bottom: 1rem;
}
.reminder{
    border-left: 6px solid forestgreen;
}
.fas{
    color: crimson;
}
</style>