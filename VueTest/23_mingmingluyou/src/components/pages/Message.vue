<template>
  <div>
      <div>
                  <ul>
                    <li v-for="m  in messageList" :key="m.id">
                      <!--跳转路由并且携带query参数，to的字符串写法--->
                      <!-- <router-link :to="`/home/message/detail/${m.id}/${m.title}`">{{m.title}}</router-link>&nbsp;&nbsp; -->
                      <!--跳转路由并且携带query参数，to的对象写法,建议使用这种方式--->
                      <router-link :to="{
                       name:'xiangqing',//可以使用name来代替path实现跳转
                       params:{
                         id:m.id,
                         title:m.title,
                       }
                      }">
                      {{m.title}}
                      </router-link>&nbsp;&nbsp;
                    </li>
                  </ul>
                  <hr>
                  <router-view></router-view>
                </div>
  </div>
</template>

<script>
export default {
    name:'Message',
    data() {
        return {
            messageList:[
                {id:'001',title:'消息001'},
                {id:'002',title:'消息002'},
                {id:'003',title:'消息003'},
            ]
        }
    },


}
</script>
