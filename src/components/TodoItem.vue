<template>
    <li class="item" v-on:click ="handleDelete">{{content}}</li>
</template>

<script>
export default {
    props:['content','index'],
    methods: {
        handleDelete(){
            //$emit触发当前实例上的事件。附加参数都会传给监听器回调。
            this.$emit('delete-item',this.index)
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    /*<!--scoped为样式添加了一个域  这里的样式只适应于本组件-->*/
    .item{
        color: skyblue;
    }

</style>
