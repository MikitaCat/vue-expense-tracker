<template>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Text</label>
            <input v-model="text" type="text" id="text" placeholder="Enter text..." />
        </div>
        <div class="form-control">
            <label for="amount">Amount <br />
                (negative - expense, positive - income)</label>
            <input v-model="amount" type="text" id="amount" placeholder="Enter amount..." />
        </div>
        <button class="btn">Add transaction</button>
    </form>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from "vue-toastification"

const toast = useToast()

const text = ref("")
const amount = ref("")

const emit = defineEmits(["transactionSubmitted"])

const onSubmit = () => {
    if (!text.value || !amount.value) {
        toast.error("Both fields should be filled")
        return
    }
    if (isNaN(parseFloat(amount.value))) {
        toast.error("Please put the number to Amount field")
        return
    }

    console.log(text.value, amount.value)
    const transactionData = {
        text: text.value,
        amount: parseFloat(amount.value)
    }

    emit("transactionSubmitted", transactionData)

    text.value = ""
    amount.value = ""

}
</script>