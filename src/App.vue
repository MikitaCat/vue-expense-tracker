<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpences :income="+income" :expense="+expense" />
    <TransactionList :transactions="transactions" @transactionDeleted="handleTranactionDeleted" />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
import Balance from './components/Balance.vue';
import Header from './components/Header.vue';
import IncomeExpences from "./components/IncomeExpenses.vue"
import TransactionList from "./components/TransactionList.vue"
import AddTransaction from "./components/AddTransaction.vue"
import { generateRandomNumber } from "./utils/randomNumber"

import { computed, ref, onMounted } from 'vue';

import { useToast } from 'vue-toastification';


const toast = useToast()

const transactions = ref([
])

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"))
  if (savedTransactions) {
    transactions.value = savedTransactions
  }
})

//Delete Transaction
const handleTranactionDeleted = (id) => {
  console.log("EMMITED DATA", id)
  transactions.value = transactions.value.filter((item) => item.id !== id)
  saveTransactionsToLocalStorage()

  toast.info("Transaction has been deleted")
}

//Get total
const total = computed(() => {
  return transactions.value.reduce((acc, item) => {
    return acc + item.amount
  }, 0)
})

//Get income
const income = computed(() => {
  return transactions.value.filter((item) => item.amount > 0).reduce((acc, item) => {
    return acc + item.amount
  }, 0).toFixed(2)
})

//Get expense
const expense = computed(() => {
  return transactions.value.filter((item) => item.amount < 0).reduce((acc, item) => {
    return acc + item.amount
  }, 0).toFixed(2)
})

//Add Transaction
const handleTransactionSubmitted = (data) => {
  transactions.value.push({
    id: generateRandomNumber(),
    text: data.text,
    amount: data.amount
  })
  saveTransactionsToLocalStorage()

  if (data.amount > 0) {
    toast.success(`Balance has been replenished by ${data.amount}$`)
  }
  if (data.amount < 0) {
    toast.warning(`The balance has been deducted by ${data.amount}$`)
  }
}

//Save transactions to localStorage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value))
}
</script>