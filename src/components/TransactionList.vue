<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li :class="transaction.amount < 0 ? 'minus' : 'plus'" v-for="transaction in transactions"
            v-bind:key="transaction.id">
            {{ transaction.text }} <span>{{ transaction.amount }}</span><button class="delete-btn">x</button>
        </li>
    </ul>
</template>

<script>
export default {
    data() {
        return {
            transactions: [
                { id: 1, text: "Flower", amount: -19.99 },
                { id: 2, text: "Salary", amount: 229.99 },
                { id: 3, text: "Phone", amount: -10 },
                { id: 4, text: "Guitar", amount: 150 },
            ]
        }
    }
}
</script>