<template>
  <div class="category">
   <h3>{{title}}</h3>
   <slot name="center">如果没有内容，默认展示这些文字</slot>  
   <slot name="footer">如果没有内容，默认展示这些文字</slot>  
   </div>
</template>

<script>
export default {
    name:"Category",
    props:['title']

}
</script>

<style scoped>
.category{
    background-color: skyblue;
    width: 200px;
    height: 300px;
}
h3{
    text-align: center;
    background-color: orange;
}
img{
  width: 100%;
}
video{
  width: 100%;
}
</style>