<template>
    <div class="contract-list">
        <div class="item-container">
            <h2>Added to Contract</h2>
            <ul id="contractList">

            </ul>
        </div>
    </div>
</template>


<script lang="ts">
import { computed, defineComponent, PropType, ref } from 'vue'
import Job from '@/types/Job'

export default defineComponent({
    props: {
        jobs: {
            type: Array as PropType<Job[]>
        }
    },
})
</script>

<style scoped>
    .contract-list {
        width: 30%;
        margin: 2.5rem 7rem 2.5rem 7rem;
    }
  .container {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: space-between;
    width: 100%;
  }

  .item-container {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 0 16px 3rem 16px;
    border-radius: 4px;
    height: 100%;
  }
</style>