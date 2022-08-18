<template>
  <div class="job-list">
    <p>Ordered by {{ order}}</p>
    <transition-group name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id" :ref="job.id" :addedProp="handleAddClick">
        <div class="container">
          <div class="container-header">
            <h2>{{ job.title}}</h2>
            <h3> in {{ job.location}}</h3>
            <div class="salary">
              <img src=".././assets/rupee.svg" alt="rupee icon" />
              <p>{{ job.salary}} rupees</p>
            </div>
          </div>
          <button @click="handleAddClick($event, job.addedToContract, job.id, job.title)" class="addItem">
            Add to Contract
          </button>
        </div>
        <div class="description">
          <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quam ad saepe ullam hic molestiae odit laborum
            distinctio aspernatur, qui excepturi dolorem quidem optio veniam cupiditate doloribus cumque recusandae nam
            deserunt!</p>
        </div>
      </li>
    </transition-group>
  </div>
</template>


<script lang="ts">
import {computed, defineComponent, PropType, ref} from 'vue'
import Job from '@/types/Job'
import OrderTerm from '@/types/OrderTerm';

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>
    },
  },
  setup(props) {
    const orderedJobs = computed(() => {
      // instead of altering the jobs prop itself
      // make a new array and spread the values to sort
      return [...props.jobs].sort((a: Job, b: Job) => {
        //since this is dynamic, put in brackets
        // basically like accessing a.location
        return a[props.order] > b[props.order] ? 1 : -1
      })
    })

    var addedProp = false;

    const handleAddClick = (event: any, addedToContractState: boolean, jobID: string, jobTitle: string) => {
      let jobContainer = event.target.parentElement.parentElement;
      let contractContainer = document.getElementById("contractList");

      if (addedToContractState === true) {
        addedToContractState = false;
      } else {
        addedToContractState = true;
        contractContainer?.append(jobContainer);
      }
      console.log(addedProp);
      return addedToContractState;
    }


    return {orderedJobs, handleAddClick};
  }
})
</script>

<style scoped>
.job-list {
  max-width: 65%;
  margin-left: 7rem;
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

.job-list h3 {
  text-transform:capitalize;
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

.list-move {
  transition: all 1s;
}

.container {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-between;
  width: 100%;
}
</style>