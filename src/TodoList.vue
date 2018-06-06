<template xmlns:v-on="http://www.w3.org/1999/xhtml" xmlns="" xmlns:v-bind="">
  <div class="container" >
    <div class="add-task">
      <h1 v-text="title"></h1>
      <input v-model="inputValue" name="content" type="text"  placeholder="e.g.今天记得学习"
             autofocus="autofocus" autocomplete="off" v-on:keyup.enter="handleSubmit">
      <button @click="handleSubmit" type="submit">提交</button>
      <button @click="handleDeleteAll" type="submit">删除全部</button>
    </div>

    <todo-item v-for = "(item,index) of list" :key="index"  :content="item" :index="index"
               v-bind:class ="{finished:item.isFinished}"
               @delete-item="handleDelete"
               @change-item="handleChange"
               @detail-item="detailShow">
    </todo-item>

</div>
</template>

<script>
import TodoItem from './components/TodoItem'
import Store from './store'
export default {
    components :{
        'todo-item': TodoItem
    },
    //使用脚手架时 data由一个对象变成一个函数
    //以下写法相当于 data : function()
    data (){   
        return{
            currentTime: '',
            title:'to do my list!',
            inputValue : '',
            list:[],
            flag: true
            // isFinished:false
            // list: Store.fetch()
        }
    },
    /*//存入localstore
    watch:{
        list :{
            handler :function (list) {
                Store.save(list)
            },
        deep:true
        }
    },*/
    methods :{
        handleSubmit (index){
              if(!this.inputValue == "") {

                var date = new Date();
                var year = date.getFullYear();
                var month = date.getMonth()+1;
                var day = date.getDate();
                var time = date.getHours();
                var minutes = date.getMinutes();
                var seconds = date.getSeconds();
                var currentTime = year+"年"+month+"月"+day+"日"+"  "+time+":"+minutes+":"+seconds
                  console.log(currentTime)
                  this.list.unshift(currentTime + "\t"+this.inputValue)
                  //this的指向是当前的实例
                  this.inputValue = ''
                   // Store.save()
              }
        },
        handleDelete (index){
            this.list.splice(index,1)
        },
        handleDeleteAll(index){
            // this.list.length = 0;
            this.list.splice(index)
        },
        handleChange(index){
            // item.isFinished = !item.isFinished
            this.list[index]
            console.log()
         },
        detailShow(index){
            var tmp = this.list[index].split("\t")
            alert(tmp[1])
            // alert(
            //     '<form>'+
            //     '<div class="content">'+
            //      "sdshkh"+
            //     '</div>'+
            //     '<div class="input_item">'+
            //     '<input style="display: none;" type="text" name="content" value="' + index + '"></div>' +
            //     '<div>'+
            //     '<div class="desc input_item">'+
            //     '<textarea  name="desc"> '+ "xxxxx" + ' </textarea>'+
            //     '</div>'+
            //     '</div>'+
            //     '<div class="remind input_item">'+
            //     '<label>提醒时间</label>'+
            //     '<input class="datetime" name="remind_date" type="text" value="'+ "xxxx" +'">'+
            //     '</div>'+
            //     '<div class="input_item"><button type="submit">更新</button></div>'+
            //     '</form>') ;
        }
      }
}
</script>

<style>
 .change{
   background-color: aqua;
   color:darkolivegreen;
 }
  *{
    /*background: rgba(0,0,0,.1);*/
    box-sizing: border-box;
    /*transition是什么作用*/
    transition: background-color .2s;
    outline: 0;
  }
 body{
   background-color: lightpink;
 }
 .container{
   max-width: 700px;
   margin: 0 auto;/*设置居中*/
   position: relative;/*为父元素添加relative，子元素设置absolute*/
   padding: 0 10px ;
 }
 h1{
   text-align: center;
 }
 .add-task input[type=text]{
   float: left;
   width: 65%;
   margin-right: 1%;
 }
 .add-task [type=submit]{
   width: 15%;
   -webkit-box-shadow: 0 2px 3px rgba(0,0,0,.4);
 }
 .add-task [type=submit]:hover{
   background: #b7a0ae;
 }
 input,button{
   border-radius: 3px;
   padding: 10px;
   border: 0;
 }
 .tmp{
     float: right;
 }
</style>

