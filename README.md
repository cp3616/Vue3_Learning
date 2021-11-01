# Vue3_Learning
2021.11.1 Dormitory 
1. 组合式API setup，与Vue2最大的区别就在于将methods和data放在了一起，更聚合
2. ref-响应式变量，reactive-响应式对象，toRef-转化成响应式变量（一个）,toRefs-转化成响应式变量（多个）,watchEffect响应式监听（会自动判断监听的哪一个）
3. 响应式监听watchEffect(()=>{}) ,单独监听watch(num,(newNum,preNum)=>{} ,多个监听watch([num,user],(newNum,preNum)=>{}
