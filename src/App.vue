<template>
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpences />
    <TransactionList />
    <AddTransaction />
  </div>
</template>

<script setup>
import Balance from './components/Balance.vue';
import Header from './components/Header.vue';
import IncomeExpences from "./components/IncomeExpenses.vue"
import TransactionList from "./components/TransactionList.vue"
import AddTransaction from "./components/AddTransaction.vue"
</script>