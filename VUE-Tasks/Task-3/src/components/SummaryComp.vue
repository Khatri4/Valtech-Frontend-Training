<script setup>
import { computed } from "vue";

const props = defineProps({
  groupName: String,
  members: Array,
});
const emit = defineEmits(["back"]);

const transactions = computed(() => {
  const creditors = [];
  const debtors = [];

  props.members.forEach(({ name, balance }) => {
    if (balance > 0) creditors.push({ name, amount: balance });
    if (balance < 0) debtors.push({ name, amount: -balance });
  });

  const results = [];
  let i = 0,
    j = 0;

  while (i < debtors.length && j < creditors.length) {
    const debtor = debtors[i];
    const creditor = creditors[j];
    const minAmount = Math.min(debtor.amount, creditor.amount);

    results.push(
      `${debtor.name} pays ${creditor.name} ₹${minAmount.toFixed(2)}`
    );

    debtor.amount -= minAmount;
    creditor.amount -= minAmount;

    if (debtor.amount === 0) i++;
    if (creditor.amount === 0) j++;
  }

  return results;
});
</script>

<template>
  <div>
    <h2>Summary for Group: {{ groupName }}</h2>

    <div v-if="transactions.length === 0">
      <p>All expenses are settled!</p>
    </div>

    <ul v-else>
      <li v-for="(txn, idx) in transactions" :key="idx">{{ txn }}</li>
    </ul>

    <br />
    <button @click="emit('back')">Back</button>
  </div>
</template>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 16px;
}

h2 {
  margin-bottom: 16px;
}

ul {
  list-style-type: none;
  padding-left: 0;
}

li {
  margin-bottom: 10px;
}

button {
  margin-top: 16px;
  padding: 8px 12px;
  cursor: pointer;
}
</style>
