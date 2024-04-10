<template>
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpences />
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<script setup>
import Balance from './components/Balance.vue';
import Header from './components/Header.vue';
import IncomeExpences from "./components/IncomeExpenses.vue"
import TransactionList from "./components/TransactionList.vue"
import AddTransaction from "./components/AddTransaction.vue"

import { ref } from 'vue';

const transactions = ref([
  { id: 1, text: "Flower", amount: -9.99 },
  { id: 2, text: "Salary", amount: 229.99 },
  { id: 3, text: "Phone", amount: -10 },
  { id: 4, text: "Guitar", amount: 150 },
])
</script>