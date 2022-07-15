<template>
  <div class="school">
    <h2>学校名称：{{name}}</h2>
    <h2>学校地址：{{address}}</h2>
  </div>
</template>
<script>

export default{
    name:'school',
    data(){
         return{
           name:'上学',
          address:"中国"
}
    }
  

}
</script>
<style scoped>
.school{
    background-color: skyblue;
}
</style>