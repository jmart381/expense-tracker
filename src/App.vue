<script setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import {computed, ref} from 'vue'

  const transactions = ref([
    {id: 1, text: 'Paycheck', amount: 699.99},
    {id: 2, text: 'Food', amount: -20},
    {id: 3, text: 'Bills', amount: -200},
    {id: 4, text: 'Video game', amount: -54.11}
  ])

  //get the total
  const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
  })


  
</script>

<template>
  <Header></Header>
  <div class="container">
    <Balance  :total="total"></Balance>
  </div>
</template>