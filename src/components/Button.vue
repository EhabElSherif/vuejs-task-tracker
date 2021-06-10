<template>
    <button @click="OnClick()" class="btn btn-primary">{{text}}</button>
</template>

<script>
export default {
    name:"Button",
    props:{
        text: String,
        type: String
    },
    methods: {
        OnClick(){
            console.log("joo")
        }
    }
}
</script>