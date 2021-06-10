<template>
	<div class="container">
		<Header @toggle-add-form="toggleForm" title="Task Tracker" :show_add_task="show_add_task" />
		<div v-if="show_add_task">
			<AddTask @add-task="addTask" />
		</div>
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
			tasks:[],
			show_add_task: false
		}
	},
	methods:{
		async deleteTask(id){
			if(confirm("Are you sure to delete this task?!!")){
				const res = await fetch(`api/tasks/${id}`,{
					method:'DELETE'
				})
				if(res.status === 200) {
					this.tasks = this.tasks.filter(task => task.id !== id)
				}else{
					alert("Error deleting this task")
				}
			}
		},
		async toggleReminder(id){
			const task_to_toggle = await fetchTask(id)
			const updTask = {...task_to_toggle, reminder:!task_to_toggle.reminder}
			
			const res = await fetch(`api/tasks/${id}`,{
				method:"PUT",
				headers:{
					'Content-type':'application/json'
				},
				body: JSON.stringfy(updTask)
			})
			const data = await res.json()
			
			this.tasks = this.tasks.map(task=>(
				task.id === id ? {...task,reminder:data.reminder} : task
			))
		},
		async addTask(new_task){
			const res = await fetch('api/tasks',{
				method:"POST",
				headers: {
					'Content-type':'application/json'
				},
				body: JSON.stringify(new_task)
			})

			const data = await res.json()
			this.tasks = [...this.tasks, data] 
		},
		toggleForm(){
			this.show_add_task = !this.show_add_task
		},
		async fetchTasks(){
			const res = await fetch('api/tasks')
			const data = await res.json()
			return data
		},
		async fetchTask(id){
			const res = await fetch(`api/tasks/${id}`)
			const data = await res.json()
			return data
		},
	},
	async created(){
		this.tasks = await this.fetchTasks()
	},
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
