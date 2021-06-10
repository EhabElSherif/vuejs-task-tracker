<template>
    <div v-if="show_add_task">
        <AddTask @add-task="addTask" />
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
</template>

<script>
import Tasks from './../components/Tasks.vue'
import AddTask from './../components/AddTask.vue'

export default {
    name:"Home",
    props:{
        show_add_task: Boolean,
    },
    components:{
        Tasks,
        AddTask
    },
    data(){
        return {
            tasks:[]
        }
    },
	methods:{
		async fetchTask(id){
			const res = await fetch(`api/tasks/${id}`)
			const data = await res.json()
			return data
		},
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
			const task_to_toggle = await this.fetchTask(id)
			const updTask = {...task_to_toggle, reminder:!task_to_toggle.reminder}
			
			const res = await fetch(`api/tasks/${id}`,{
				method:"PUT",
				headers:{
					'Content-type':'application/json'
				},
				body: JSON.stringify(updTask)
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
		async fetchTasks(){
			const res = await fetch('api/tasks')
			const data = await res.json()
			return data
		},
	},
	async created(){
		this.tasks = await this.fetchTasks()
	},
}
</script>