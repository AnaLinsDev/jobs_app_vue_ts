<template>
  <div class="app">
    <header>
      <div class="order">
        <p class="order-info">
          Ordenar por: 
        </p>
        <button @click="orderBy('title')">Título</button>
        <button @click="orderBy('salary')">Salário</button>
        <button @click="orderBy('location')">Localização</button>
      </div>
    </header>

    <JobListComponent :jobs="jobs" :order="order" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import Job from './types/Job'
import OrderTerm from './types/OrderTerm'
import JobListComponent from './components/JobListComponent.vue'

export default defineComponent({
  name: 'App',
  components: { JobListComponent },

  setup() {
    /*
    const state = reactive({
      name: 'Link',
      age: 25 as number | string
    })

    return {
      ...toRefs(state)
    }
    */

    const order = ref<OrderTerm>('title')

    const orderBy = (term: OrderTerm) => {
      order.value = term
    }

    const jobs = ref<Job[]>([
      { title: 'trabalhador rural', location: 'fazenda lon lon', salary: 3000, id: '1' },
      { title: 'canteiro', location: 'montanha da morte', salary: 4000, id: '2' },
      { title: 'tocador de flauta', location: 'floresta perdida', salary: 3000, id: '3' },
      { title: 'pescador', location: 'lago hylia', salary: 2100, id: '4' },
      { title: 'guarda de prisão', location: 'vale gerudo', salary: 3200, id: '5' }
    ])

    return { jobs, orderBy, order }
  }
})
</script>

<style>
.order-info {
  color: whitesmoke;
  font-weight: bold;
}

header {
  text-align: center;
}
header .order {
  margin-top: 20px;
}
button {
  margin: 0 10px;
  border: 3px solid #9eecbb;
  background:whitesmoke;
  padding: 8px 16px;
  border-radius: 5px;

  cursor: pointer;
  font-weight: 800;
}
</style>
