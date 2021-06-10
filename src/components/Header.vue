<template>
    <header class="d-flex justify-content-between align-items-center my-3">
        <h1 class="m-0">{{title}}</h1>
        <Button v-show="homePage" @btn-click="$emit('toggle-add-form')" :text="show_add_task? 'Close' : 'Add Task'" :type="show_add_task? 'danger' : 'primary'" :show_add_task="show_add_task" />
    </header>
</template>

<script>
import Button from './Button.vue'

export default {
    name: "Header",
    components: {
        Button
    },
    props: {
        title: String,
        show_add_task: Boolean
    },
    computed: {
        homePage(){
            if(this.$route.path==='/'){
                return true
            }else{
                return false
            }
        }
    }
}
</script>

<style scoped>
</style>