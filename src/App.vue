<template>
	<div class="container">
		<Header @toggle-add-form="toggleForm" title="Task Tracker" :show_add_task="show_add_task" />
		<router-view :show_add_task="show_add_task"></router-view>
		<Footer />
	</div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';
import '@fortawesome/fontawesome-free/css/all.css';
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'


export default {
	name: 'App',
	components: {
		Header,
		Footer,
	},
	data(){
		return {
			show_add_task: false
		}
	},
	methods:{
		toggleForm(){
			this.show_add_task = !this.show_add_task
		},
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
