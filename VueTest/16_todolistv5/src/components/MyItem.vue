<template>
        <li>
          <label>
            <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)"/>
            <span v-show="!todo.isEdit">{{todo.title}}</span>
            <input v-show="todo.isEdit" type="text" :value="todo.title" @blur="endEdit(todo,$event)" ref="inputTitle"/>
          </label>
          <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
          <button v-show="!todo.isEdit" class="btn btn-edit" @click="handleEdit(todo)">编辑</button>
        </li>
</template>

<script>
import pubsub from 'pubsub-js'
export default {
name:"MyItem",
//生命接收todo对象
props:['todo'],
methods: {
  //勾选or 反选
  handleCheck(id){
  this.$bus.$emit('checkTodo',id)
  },
  //删除事件
  handleDelete(id){
  if(confirm("确定删除吗？")){
  pubsub.publish('deleteTodo',id)
  }
  },
  //编辑
  handleEdit(todo){
  if(todo.hasOwnProperty('isEdit')){
     todo.isEdit=true
  }else{
   this.$set(todo,'isEdit',true)
  }
  //nexttick在解析模板，DOM更新完毕以后执行
  this.$nextTick(function(){
  this.$refs.inputTitle.focus()
  })
  },
  //失去焦点回调
  endEdit(todo,e){
  todo.isEdit=false
  if(!e.target.value)return alert('输入不能')
  this.$bus.$emit('updateTodo',todo.id,e.target.value)
  
  }
},
}
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
li:hover button{
  display: block;
}
</style>