<script lang="ts">
import { defineComponent, computed, type PropType } from 'vue';
import type Job from '@/types/job';
import type OrderTerm from '@/types/OrderTerm';

// const { jobs, order } = defineProps({
//   jobs: Array as PropType<Job[]>,
//   order: String as PropType<OrderTerm>,
// });

// const orderedJobs = computed(() => {
//   if (!jobs || jobs.length === 0 || !order) {
//     return [];
//   }
//   return [...jobs].sort((a: Job, b: Job) => {
//     return a[order] > b[order] ? 1 : -1;
//   });
// });

export default defineComponent({
  props: {
    jobs: {
      type: Array as PropType<Job[]>,
      required: true
    },
    order: {
      type: String as PropType<OrderTerm>,
      required: true
    }
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1
      })
    })

    return { orderedJobs }
  },
})

</script>
<template>
  <div class="job-list">
    <p>Ordered by {{ order }}</p>
    <p>{{ orderedJobs }}</p>
    <ul>
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }} in {{ job.location }}</h2>
        <div class="salary">
          <p>${{ job.salary }}</p>
        </div>
        <div class="description">
          <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Rem omnis voluptatum eius
            doloremque optio iusto sequi dignissimos. Pariatur earum assumenda dolores possimus
            quidem quam, reprehenderit aliquid consequuntur amet non facere.
          </p>
        </div>
      </li>
    </ul>
  </div>
</template>
<style scoped>
.job-list {
  max-width: 960px;
  margin: 40px auto;
}
.job-list ul {
  padding: 0;
}
.job-list li {
  list-style-type: none;
  background: white;
  padding: 16px;
  margin: 16px 0;
  border-radius: 4px;
}
.job-list h2 {
  margin: 0 0 10px;
  text-transform: capitalize;
}
.salary {
  display: flex;
}
.salary img {
  width: 30px;
}
.salary p {
  color: #17bf66;
  font-weight: bold;
  margin: 10px 4px;
}
</style>
