<template>
    <h3>Add A New Transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Text</label>
            <input type="text" id="text" v-model="text" placeholder="Enter Text...">
        </div>

        <div class="form-control">
            <label for="amount">amount(negative - expense, positive - income)</label>
            <input type="text" id="amount" v-model="amount" placeholder="Enter Amount...">
        </div>
        <!-- {{ text }} -{{ amount }} -->
        <button class="btn">Add Transaction</button>
    </form>
</template>

<script setup>
import{ref, defineEmits} from 'vue'
import {useToast} from 'vue-toastification'
const text = ref('')
const amount = ref('')
const toast = useToast()

const emit = defineEmits([
    'transactionSubmitted'
])

const onSubmit = () => {

    // check if both fields are filled
    if(!text.value || !amount.value)
    {
        toast.error('Both fields must be filled')
        return
    }
    const transactionData = {
        text: text.value,
        amount: parseFloat(amount.value),
    }

    emit('transactionSubmitted', transactionData)

    text.value = ''
    amount.value = ''

}
</script>
