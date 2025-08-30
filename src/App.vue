<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExp :income="+income" :expense="+expense" />
    <Transaction
      :transactions="transactions"
      @transectiondelete="handletransectiondelete"
    />
    <AddTrans @transectionSumitted="handletransectiosubmited" />
  </div>
</template>
<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExp from "./components/IncomeExp.vue";
import Transaction from "./components/Transaction.vue";
import AddTrans from "./components/AddTrans.vue";
import { ref, computed, onMounted } from "vue";
import { useToast } from "vue-toastification";
const toast = useToast();

const transactions = ref([
  // { id: 1, text: "Flower", amount: -29.939 },
  // { id: 2, text: "Flower", amount: -19.929 },
  // { id: 3, text: "Flower", amount: 29.993 },
  // { id: 4, text: "Flower", amount: 39.949 },
]);
onMounted(() => {
  const savedTransaction = JSON.parse(localStorage.getItem("transactions"));
  if (savedTransaction) {
    transactions.value = savedTransaction;
  }
});

const total = computed(() => {
let exp=  transactions.value
    .filter((t) => t.type=='expense')
    .reduce((acc, tran) => {
      return acc + tran.amount;
    }, 0)
    .toFixed(2);
let inc=  transactions.value
    .filter((t) => t.type=='income')
    .reduce((acc, tran) => {
      return acc + tran.amount;
    }, 0)
    .toFixed(2);

    return inc-exp
});
const income = computed(() => {
  return transactions.value
    .filter((t) => {
      return t.type=='income'})
    .reduce((acc, tran) => {
      return acc + tran.amount;
    }, 0)
    .toFixed(2);
});
const expense = computed(() => {
  return transactions.value
    .filter((t) => t.type=='expense')
    .reduce((acc, tran) => {
      return acc + tran.amount;
    }, 0)
    .toFixed(2);
});
const generateId = () => {
  let last = transactions.value[transactions.value.length - 1];
  const fid = last ? last.id + 1 : 1; //
  console.log(last);
  return fid;
};

const handletransectiosubmited = (transectiondata) => {
  console.log(transectiondata);
  transactions.value.push({
    id: generateId(),
    text: transectiondata.text,
    amount: transectiondata.amount,
    type: transectiondata.type,
  });
  toast.success("Transection Added Successfully");
  saveLocal()
};

const handletransectiondelete = (id) => {
  console.log(id);
  transactions.value = transactions.value.filter((e) => e.id !== id);
  saveLocal()

};

const saveLocal=()=>{
  localStorage.setItem('transactions',JSON.stringify(transactions.value))
}

console.log(income.value, expense.value);
</script>
