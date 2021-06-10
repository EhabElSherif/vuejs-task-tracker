<template>
	<div class="container">
		<Header title="Task Tracker" />
		<AddTask @add-task="addTask" />
		<Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
	</div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';
import '@fortawesome/fontawesome-free/css/all.css';
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'


export default {
	name: 'App',
	components: {
		Header,
		Tasks,
		AddTask,
	},
	data(){
		return {
			tasks:[]
		}
	},
	created(){
		this.tasks = [
			{
				id: 1,
				text: "task text 1",
				day: "March 1st at 2:20pm",
				reminder: true,
			},
			{
				id: 2,
				text: "task text 2",
				day: "March 2st at 2:20pm",
				reminder: false,
			},
			{
				id: 3,
				text: "task text 3",
				day: "March 3st at 2:20pm",
				reminder: true,
			},
			{
				id: 4,
				text: "task text 4",
				day: "March 4st at 2:20pm",
				reminder: false,
			},
		]
	},
	methods:{
		deleteTask(id){
			if(confirm("Are you sure to delete this task?!!")){
				this.tasks = this.tasks.filter(task => task.id !== id)
			}
		},
		toggleReminder(id){
			this.tasks = this.tasks.map(task=>(
				task.id === id ? {...task,reminder:!task.reminder} : task
			))
		},
		addTask(new_task){
			this.tasks = [...this.tasks,new_task] 
		}
	}
}
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: #2c3e50;
}
</style>
