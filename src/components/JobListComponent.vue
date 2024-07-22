<template>
  <div class="job-list">
    <ul>
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }} em {{ job.location }}</h2>
        <div class="salary">
          <p>{{ job.salary }} R$ Monthly</p>
        </div>
        <div class="description">
          <p class="description-text">
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Rem omnis voluptatum eius
            doloremque optio iusto sequi dignissimos. Pariatur earum assumenda dolores possimus
            quidem quam, reprehenderit aliquid consequuntur amet non facere.
          </p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from 'vue'
import Job from '@/types/Job'
import OrderTerm from '@/types/OrderTerm';

export default defineComponent({
  name: 'JobListComponent',
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

<style scoped>

.description-text {
  text-align: justify;
}

.job-list {
  max-width: 960px;
  margin: 40px auto;
}
.job-list ul {
  padding: 0;
}
.job-list li {
  list-style-type: none;
  background: whitesmoke;
  padding: 16px 30px;
  margin: 16px 0;
  border-radius: 8px;
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
  margin: 8px 4px;
}
</style>
