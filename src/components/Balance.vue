<template>
  <h4>Your Balance</h4>
  <h1 id="balance" :class="total>0?'bal-green':'bal-red'">₹{{ total.toFixed(2) }}</h1>
</template>

<script setup>
import { defineProps } from "vue";

const prop = defineProps({
  total: { type: Number, required: true },
});
</script>
