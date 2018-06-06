<template>
    <input
            type="checkbox"
            v-bind:checked="checked"
            v-on:change="$emit('change', $event.target.checked)"
    >

</template>


<script>
export default {
    model:{
        prop: 'checked',
        event: 'change'
    },
    props: {
        checked: Boolean
    },
    }
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    /*<!--scoped为样式添加了一个域  这里的样式只适应于本组件-->*/

</style>
