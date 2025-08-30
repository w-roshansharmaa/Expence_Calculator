<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }} <span>{{ transaction.amount.toFixed(2) }}</span
      ><button class="delete-btn" @click="tranctiondeletv(transaction.id)">x</button>
    </li>
    <!-- <li class="minus">
      Cash <span>-$400</span><button class="delete-btn">x</button>
    </li>
    <li class="plus">
      Paychek <span>-$400</span><button class="delete-btn">x</button>
    </li> -->
  </ul>
</template>

<script setup>
// import Tr

import { defineProps } from "vue";
const prop = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});


const emit = defineEmits(['transectiondelete'])
const tranctiondeletv=(id)=>{
  emit('transectiondelete',id)
  
}

// const prop=defineProps
</script>


<style>
.minus,.plus{
  /* border-radius: rem; */
  border-radius: 0 1rem  0 0;

}
</style>