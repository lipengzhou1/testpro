<template>
<div id="root">

<div class="todo-container">
  <div class="todo-wrap">
    <MyHeader @addTodo="addTodo" />
    <MyList :todos="todos"/>
  <MyFooter :todos="todos" @checkAllTodo="checkAllTodo" @clearAllTodo="clearAllTodo"/>
  </div>

</div>
</div>
  
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
//import pubsub from 'pubsub-js'
import MyHeader from './components/MyHeader'
import MyList from './components/MyList'
import MyFooter from './components/MyFooter'

export default {
  name: 'App',
  components:{
    MyHeader,MyList,MyFooter
  },
   data(){
        return{
            todos:[
                {id:'001',title:'吃饭',done:true},
                {id:'002',title:'睡觉',done:false},
                {id:'003',title:'打豆豆',done:true}
            ],
        }
    },
   methods:{
    addTodo(todoobj){
      this.todos.unshift(todoobj)
      // console.log("6666")
      
    },
  checkTodo(id){
        //console.log(id)
        this.todos.forEach((todo)=>{
          if(todo.id===id) todo.done=!todo.done
        })
   

   } ,
    updateTodo(id,title){
        //console.log(id)
        this.todos.forEach((todo)=>{
          if(todo.id===id) todo.title=title
        })
   

   } ,
   deleteTodo(id){
   this.todos=this.todos.filter((todo)=>{
   return todo.id!==id
    })
   },
   checkAllTodo(done){
    this.todos.forEach((todo)=>{
        todo.done=done
    })
    },
    clearAllTodo(){
      this.todos=this.todos.filter((todo)=>{
        return !todo.done
      })
    }
   },
   mounted(){
    this.$bus.$on('checkTodo',this.checkTodo)
    this.$bus.$on('deleteTodo',this.deleteTodo)
    this.$bus.$on('updateTodo',this.updateTodo)
   // this.pubid=pubsub.subscribe('deleteTodo',this.deleteTodo)
   },
   beforeDestroy(){
    this.$bus.$off('checkTodo')
    this.$bus.$off('deleteTodo')
    this.$bus.$off('updateTodo')
//pubsub.unsubscribe( this.pubid)
   }

   }
</script>

<style>
body{
  background-color:#fff;
}
.btn{
  display:inline-block;
  padding:4px 12px;
  margin-bottom:0;
  font-size:14px;
  line-height:20px;
  text-align:center;
  vertical-align:middle;
  cursor:pointer;
  box-shadow:inset 0 1px 0 rgba(255,255,255,0.2),0 1px 2px rgba(0,0,0,0.4);
  border-radius:4px;
}
.btn-danger{
color:white;
 background-color: #bd362f;
border:1px solid white
}
.btn-edit{
color:black;
 background-color:aqua;
border:1px solid white
}
.btn-danger:hover{
  color:#fff;
  background-color: #bd362f;
}
.btn:focus{
  outline:none;
}
.todo-container{
  width:600px;
  margin:0 auto;
}
.todo-container .todo-wrap{
  padding:10px;
  border:1px solid #ddd;
  border-radius:5px;
}
</style>
