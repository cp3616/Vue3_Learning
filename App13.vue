
<template>
<div>
  <h1 @click="changeEvent">计数：{{ count }}</h1>
  <h1 @click="changeNum">计数：{{ num }}</h1>

  <!-- 采用reactive响应式对象 -->
  <h1>用户名：{{user.usersname}}</h1>
  <h1>特点：{{user.type}}</h1>

  <!-- 升级，采用toRefs+reactive，结构后的响应式对象 -->
  <h1>用户名：{{usersname}}</h1>
  <h1 @click="changeType">特点：{{type}}</h1>  
  <h1>特点翻转：{{reverseType}}</h1>
</div>
</template>

<script>
// ref-响应式变量，reactive-响应式对象，toRef-转化成响应式变量（一个）,toRefs-转化成响应式变量（多个）,watchEffect响应式监听（会自动判断监听的哪一个）
import {ref,toRefs,reactive,computed,watchEffect, watch} from 'vue'

export default {
  data(){
    console.log('data')
    return{
      count:0
    }
  },
  methods:{
    changeEvent(){
      this.count+=1
    }
  },

  // 组合式API setup，与Vue2最大的区别就在于将methods和data放在了一起，更聚合
  setup(){
    console.log('setup')
    const num=ref(0)
    const user=reactive({
      usersname:'wy',
      age:'30',
      type:'hansome',
      reverseType:computed(()=>{
        return user.type.split('').reverse().join('')
      })
    })
    function changeNum(){
      num.value+=10
    }
    function changeType(){
      user.type='more hansome'
    }

    // 响应式监听
    watchEffect(()=>{
      console.log(user.type)
      console.log('当userType改变时候，会触发执行此函数')
    })
    // 单独监听
    watch(num,(newNum,preNum)=>{
      console.log(newNum,preNum)
      console.log('当num改变时，会执行此函数')
    })
    // 多个监听
    watch([num,user],(newNum,preNum)=>{
      console.log('当num或者user改变时，会执行此函数')
    })
    return{num,changeNum,user,...toRefs(user),changeType}
  },


  beforeCreate(){
    console.log('beforCreated')
  },
  created(){
    console.log('created')
  },
  beforeMount(){
    console.log('beforeMounted')
  },
  mounted(){
    console.log('mounted')
  }
}
</script>