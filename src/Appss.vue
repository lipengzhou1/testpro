<template>
 <div class="app1">
    <h1>{{msg}}</h1>
   <School/>
   <Student/>
   </div>
</template>

<script>
import Student from './components/Student'
import School from './components/School'

export default {
  name:'Appss',
  
   components:{School,Student},
   data(){
    return{
        msg:"你好啊"
    }
   }
   
   }
</script>

<style>
.app1{
background-color:gray;
}
</style>