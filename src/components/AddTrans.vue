<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" placeholder="Enter text..." v-model="text" />
    </div>
    <div class="form-control">
      <label for="amount" 
        >Amount <span class="note"> (Use <span class="minus"> Minus(-)</span> For expense)</span>
      </label>
      <input
        type="text"
        id="amount"
        placeholder="Enter amount..."
        v-model="amount"
      />
    </div>
    <button class="btn submitbtn" >Add transaction</button>
  </form>
</template>
<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";
const toast = useToast();
const emit = defineEmits(['transectionSumitted'])
const text = ref("");
const amount = ref("");
const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error("Both Filds are Required");
    return;
  }
  console.log("submit", text.value, amount.value);
  if ( isNaN(Number(amount.value))) {
    toast.error("Enter a valid Number");
    return;
  }

  const transectiondata={
    text:text.value,
    amount:parseFloat( amount.value)
  }
emit('transectionSumitted',transectiondata)
  text.value = "";
  amount.value = "";
};
</script>

<style setup>
.submitbtn {
  margin: 1rem auto;
  width: 80%;
  border-radius: 2rem;
  padding: .5rem !important;
  &:hover {
  }
}
.note{
  color: blue
}
.plus{
  color: #2ecc71;
  font-weight: 600;
}
.minus{
  color: #c0392b;
  font-weight: 600;
}
.btn:hover{
  background: #7157f6;
}
</style>
