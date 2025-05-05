<script setup>
import { ref, computed } from "vue";

const props = defineProps({ group: Object });
const emit = defineEmits(["back", "show-summary"]);

const billAmount = ref(0);
const payments = ref({});
const calculated = ref(false);

props.group.members.forEach((name) => {
  payments.value[name] = 0;
});

const perPersonShare = computed(() => {
  return props.group.members.length > 0 && billAmount.value
    ? billAmount.value / props.group.members.length
    : 0;
});

const contributions = computed(() => {
  return props.group.members.map((member) => {
    const paid = payments.value[member] || 0;
    const share = perPersonShare.value;
    return {
      name: member,
      paid,
      share,
      balance: paid - share,
    };
  });
});

function calculate() {
  if (billAmount.value <= 0) return alert("Enter valid bill");
  calculated.value = true;
}

function goToSummary() {
  emit("show-summary", {
    groupName: props.group.name,
    members: contributions.value,
  });
}
</script>

<template>
  <div>
    <h2>Expenses for Group: {{ group.name }}</h2>

    <label>Total Bill Amount:</label>
    <input type="number" v-model.number="billAmount" />

    <h3>How much did each member pay?</h3>
    <ul>
      <li v-for="member in group.members" :key="member">
        {{ member }} paid:
        <input type="number" v-model.number="payments[member]" />
      </li>
    </ul>

    <button @click="calculate">Calculate</button>

    <div v-if="calculated">
      <h3>Per Person Share: ₹{{ perPersonShare.toFixed(2) }}</h3>

      <table border="1" cellpadding="8" cellspacing="0">
        <thead>
          <tr>
            <th>Member</th>
            <th>Paid</th>
            <th>Should Pay</th>
            <th>Balance</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="entry in contributions" :key="entry.name">
            <td>{{ entry.name }}</td>
            <td>₹{{ entry.paid }}</td>
            <td>₹{{ entry.share.toFixed(2) }}</td>
            <td>
              <span v-if="entry.balance > 0"
                >Gets ₹{{ entry.balance.toFixed(2) }}</span
              >
              <span v-else-if="entry.balance < 0"
                >Owes ₹{{ (-entry.balance).toFixed(2) }}</span
              >
              <span v-else>Settled</span>
            </td>
          </tr>
        </tbody>
      </table>

      <button @click="goToSummary">Show Summary</button>
    </div>

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

input,
select {
  margin: 8px 0;
  padding: 8px;
  width: 100px;
  box-sizing: border-box;
}

button {
  margin-top: 12px;
  padding: 8px 12px;
  cursor: pointer;
}

.member-list {
  margin-top: 16px;
  border-top: 1px solid #eee;
  padding-top: 16px;
}
</style>
