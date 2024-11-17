<template>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Text</label>
            <input type="text" id="text" v-model="text" placeholder="Enter text...">
        </div>
        <div class="form-control">
            <label for="amount">Amount <br/> (negative - expense, positive - income)</label>
            <input type="text" id="amount" v-model="amount" placeholder="Enter amount...">
        </div>
        <button class="btn">Add transaction</button>
    </form>
</template>

<script setup>
import { ref } from 'vue';
import {useToast} from 'vue-toastification';

// defining the variables for the form values
const text = ref('');
const amount = ref('');

// emitting event to change values in App.vue
const emit = defineEmits(['transactionSubmitted']);

// settng up toast for validation
const toast = useToast();

// submit function for the form submit
const onSubmit = () => {
    if(!text.value || !amount.value){
        toast.error('Both fields must be filled');
        return;        
    }

    const transactionData = {
        text: text.value,
        amount: parseFloat(amount.value)
    };

    emit('transactionSubmitted', transactionData);

    text.value = '';
    amount.value = '';
}
</script>