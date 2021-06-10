<template>
    <header class="d-flex justify-content-between align-items-center my-3">
        <h1 class="m-0">{{title}}</h1>
        <Button text="Press Here" type="primary" />
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
    }
}
</script>

<style scoped>
</style>