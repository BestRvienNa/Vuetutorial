<template>
  <div class="student">
      <h2 >学生姓名：{{name}}</h2>
      <h2>学生性别：{{sex}}</h2>
      <button @click="sendStudentName">把学生名给School组件</button>
  </div>
</template>

<script>
export default {
name :"Student",
data:function(){
    return{
        name:"张三",
        sex:"男"
    }
},
methods: {
    sendStudentName(){
        this.$bus.$emit("test",this.name)
    }
},
}
</script>
<style lang="less" scoped>
.student{
    background-color: orange;
    padding: 5px;
    margin-top: 30px;
}
</style>
