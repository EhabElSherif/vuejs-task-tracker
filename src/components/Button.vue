<template>
    <button @click="OnClick()" :class="`btn btn-`+type">{{text}}</button>
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
            this.$emit('btn-click')
        }
    }
}
</script>