<template>
   <div class="job-list">
      <p>ordered by {{order}}</p>
      <transition-group name="list" tag="ul">
         <li v-for="job in orderedJobs" :key="job.id">
            <h2>{{job.title}} in {{job.location}} </h2>
            <div class="job-salary">
               <p>{{job.salary}} $  </p>
            </div>
            <div class="descriotion">
               <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Temporibus eos dolores aliquid minima repudiandae velit veritatis corporis? Veniam laboriosam vel ipsam nam atque accusamus voluptas magni iste repellendus. Explicabo, incidunt!</p>
            </div>
         </li>
      </transition-group>
   </div>
</template>
<script lang="ts">
import Job from '@/types/job'
import OrderTerm from '@/types/OrderTerm'
import { computed, defineComponent, PropType } from 'vue'

export default defineComponent({
   props:{
      jobs:{
         type: Array as PropType<Job[]>,
         required:true,
      },
      order:{
         type: String as PropType<OrderTerm>,
         required:true,
      }
   },
   setup(props){
      const orderedJobs = computed(() => {
         return [...props.jobs].sort((a:Job,b:Job)=> {
            return a[props.order] > b[props.order] ? 1 : -1
         })
      })
      return{
         orderedJobs
      }
   },
})
</script>
<style scoped>
.job-list{
   max-width: 960px;
   margin: 40px auto;
}
li{
   padding:16px;
   border-radius: 4px;
   margin-bottom: 16px;
   background: #fff;
}
h2{
   margin:0 0 10px;
   text-transform: capitalize;
}
.job-salary{
   display: flex;
   margin-bottom: 16px;
   color: rgb(0, 173, 0);
}
.list-move{
   transition: all 1s linear;
}
</style>