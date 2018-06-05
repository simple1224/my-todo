<template>
<div>
  <div>
    <input v-model="inputValue">
    <button @click="handleSubmit">提交</button>
  </div>
  <ul>
    <todo-item v-for = "(item,index) of list" :key="index"  :content="item" :index="index" @delete-item="handleDelete">
    </todo-item>

  </ul>
</div>
</template>

<script>
import TodoItem from './components/TodoItem'
export default {
    components :{
        'todo-item': TodoItem
    },
    //使用脚手架时 data由一个对象变成一个函数
    //以下写法相当于 data : function()
    data (){
        return{
            inputValue : '',
            list:[]
        }
    },
    methods :{
        handleSubmit (){
           this.list.push(this.inputValue)
            //this的指向是当前的实例
            this.inputValue = ''
        },
        handleDelete (index){
            this.list.splice(index,1)
        }
    }
}
</script>

<style>

</style>
