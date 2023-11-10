<template>
  <div class="app">
    <div class="tools">
      <button @click="handleClick('title')">order by title</button>
      <button @click="handleClick('salary')">order by salary</button>
      <button @click="handleClick('location')">order by location</button>
    </div>
    <job-list :jobs="jobs" :order="order"/>
  </div>
</template>
<script  lang='ts'>
import {defineComponent, reactive, ref, toRefs} from 'vue'
import Job from '@/types/job'
import OrderTerm from '@/types/OrderTerm'
import JobList from './components/JobList.vue'
export default defineComponent({
    name:'App',
    components:{JobList},
    setup(){
      const order = ref<OrderTerm>('title')
      const jobs = ref<Job[]>([
        {title:"farm woker", location: "long long ranch", salary: 30, id:'1'},
        {title:"factory woker", location: "middle factory", salary: 40, id:'2'},
        {title:"farm woker", location: "long long ranch", salary: 20, id:'3'},
        {title:"developer", location: "not long office", salary: 50, id:'4'},
        {title:"lorry driver ", location: "in  large garage", salary: 35, id:'5'},
      ])
      const handleClick = (term:OrderTerm) => {
        order.value = term        
      }
      
      return{
        jobs,handleClick,order
      }
    },
    
})
</script>


