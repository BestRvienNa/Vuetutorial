<template>
<div>
  <h1>当前求和为:{{sum}}</h1>
  <h3>放大10倍后的和为:{{bigSum}}</h3>
  <h3>我在{{school}}学习{{subject}}</h3>
  <select v-model="n">
  <option :value="1">1</option>
  <option :value="2">2</option>
  <option :value="3">3</option>
  </select>
  <button @click="increment">+</button>
  <button @click="decrement">-</button>
  <button @click="incrementOdd">当前求和为奇数再加</button>
  <button @click="incrementWait">等一等再加</button>
</div>
</template>

<script>
//mapState用于生成属性对应的代码
import {mapState,mapGetters} from 'vuex'
export default {
    name:"Count",
    data() {
        return {
            n:1,//用户选择的数字
        }
    },
    computed:{
     //靠人工亲自生成计算属性
    /*  sum(){
            return $store.state.sum
      },
      school(){
         return $store.state.school
      },
      subject(){
          return $store.state.subject
      },
      bigSum(){
         return $store.getters.bigSum
      }*/
      //第一种借助mapState生成计算属性，从state中读取数据（对象写法）
      //...mapState({he:'sum',xuexiao:'school',xueke:'subject'}),//...代表把mapstate里面返回的对象一步步展开，放入computed中
      //第二种借助mapState生成计算属性，从state中读取数据（数组写法）
      ...mapState(['sum','school','subject']),
      /*********************mapGetters*****************************/
      //借助mapGetters生成计算属性，从getters读取数据（对象写法）
      ...mapGetters(['bigSum'])
      },
    methods: {
        increment(){
         this.$store.commit('JIA',this.n)
        },
        decrement(){
        this.$store.commit('JIAN',this.n)
        },
        incrementOdd(){
        this.$store.dispatch('jiaOdd',this.n)
        },
        incrementWait(){
         this.$store.dispatch('jiaWait',this.n)
        }
    },
    mounted(){
        const x=mapState({he:'sum',xuexiao:'school',xueke:'subject'})
        console.log(x)
    },
}
</script>

<style>
button{
    margin-left: 5px;
}
</style>