
<template>
<div>
  <h1 @click="changeEvent">计数：{{ count }}</h1>
  <h1 @click="changeNum">计数：{{ num }}</h1>
</div>
</template>

<script>
import {ref} from 'vue'

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
    function changeNum(){
      num.value+=10
    }
    return{num,changeNum}
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