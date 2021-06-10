<template>
	<div class="container">
		<Header title="Task Tracker" />
	</div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';
import '@fortawesome/fontawesome-free/css/all.css';
import Header from './components/Header.vue'

export default {
	name: 'App',
	components: {
		Header
	}
}
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
}
</style>
