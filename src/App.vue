<template>
  <div class="app">
    <header>
      <div class="title">
        <img src="./assets/heart.svg" alt="site logo"/>
        <h1>Hyrule Jobs</h1>
      </div>
      <div class="order">
        <button @click="handleClick('title')">order by title</button>
        <button @click="handleClick('salary')">order by salary</button>
        <button @click="handleClick('location')">order by location</button>
      </div>
    </header>
    <section class="home-container">
      <JobList :jobs="jobs" :order="order"/>
      <ContractList />
    </section>
  </div>

</template>

<script lang="ts">
import { computed, defineComponent, reactive, ref,  toRefs } from 'vue';
import JobList from './components/JobsList.vue';
import ContractList from './components/ContractList.vue'
import Job from './types/Job';
import OrderTerm from './types/OrderTerm';

export default defineComponent({
  name: 'App',
  components: { JobList, ContractList },
  setup() {
    // const state = reactive({
    //   name: 'Link',
    //   age: 25 as number | string
    // })

    // state.name = 'Steve' //cannot change type
    // state.age = 26;

    // return {...toRefs(state)}

    // const name = ref('Link')
    //passes type into ref to override default inferred type
    // const age = ref<number | string>(25)

    // return {name, age}

    const jobs = ref<Job[]>([
      { title: 'farm worker', location: 'lon lon ranch', salary: 30000, id: '1', addedToContract: false},
      { title: 'quarryman', location: 'death mountain', salary: 40000, id: '2', addedToContract: false},
      { title: 'flute player', location: 'the lost woods', salary: 35000, id: '3', addedToContract: false},
      { title: 'fisherman', location: 'lake hylia', salary: 21000, id: '4', addedToContract: false},
      { title: 'prison guard', location: 'gerudo valley', salary: 32000, id: '5', addedToContract: false},
    ])
    const order = ref<OrderTerm>('title');

    const handleClick = (term: OrderTerm) => {
      order.value = term;
    }

    return { jobs, handleClick, order }
  },

});
</script>

<style>
    header {
      text-align: center;
    }
    header .order {
      margin-top: 20px;
    }
    header .title {
      display: flex;
      justify-content: center;
    }
    header img {
      width: 60px;
      margin-right: 20px;
    }
    header h1 {
      font-size: 3em;
    }
    button {
      margin: 0 10px;
      color: #1195c9;
      border: 3px solid #1195c9;
      background: #d5f0ff;
      padding: 8px 16px;
      border-radius: 4px;
      cursor: pointer;
      font-weight: bold;
      max-height: 3rem;
      text-transform: capitalize;
    }
    .home-container {
      display: flex;
      flex-direction: row;
      flex-wrap: nowrap;
      justify-content: space-between;
    }
</style>
