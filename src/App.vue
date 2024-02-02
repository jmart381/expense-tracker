<script setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import IncomeExpenses from './components/IncomeExpenses.vue';
  import AddTransaction from './components/AddTransaction.vue';
  import TransactionList from './components/TransactionList.vue';
  import {computed, ref} from 'vue'

  const transactions = ref ([])
  // const transactions = ref([
  //   {id: 1, text: 'Paycheck', amount: 699.99},
  //   {id: 2, text: 'Food', amount: -20},
  //   {id: 3, text: 'Bills', amount: -200},
  //   {id: 4, text: 'Video game', amount: -54.11}
  // ])

  //get the total
  const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
  })


  //get income by adding positive values
const income = computed( () => {
  return transactions.value
  .filter((transaction) => transaction.amount > 0)
  .reduce( (acc, transaction) => {
    return acc + transaction.amount
  }, 0)
})

//get the expense by adding negative values
const expense = computed( () => {
  return transactions.value
  .filter((transaction) => transaction.amount < 0)
  .reduce( (acc, transaction) => {
    return acc + transaction.amount
  }, 0)
})

//handle transactions submitted
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  })
}


// generate unique id
const generateUniqueId = () => {
  return Math.floor(Math.random() * 10000000)
}

</script>

<template>
  <Header></Header>
  <div class="container">
    <Balance  :total="total"></Balance>
    <IncomeExpenses :income="income" :expense="expense"></IncomeExpenses>
    <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"></TransactionList>

    <AddTransaction @transactionSubmitted="handleTransactionSubmitted"></AddTransaction>
    <!-- {{ transactions }} -->
  </div>
</template>