<script setup>
import { ref, watch } from "vue";
import HomeComp from "./components/HomeComp.vue";
import ExpenseComp from "./components/ExpenseComp.vue";
import SummaryComp from "./components/SummaryComp.vue";

const currentScreen = ref("home");
const selectedGroup = ref(null);
const summaryData = ref(null);

const groups = ref(JSON.parse(localStorage.getItem("groups")) || []);

watch(
  groups,
  (newGroups) => {
    localStorage.setItem("groups", JSON.stringify(newGroups));
  },
  { deep: true }
);

function goToExpenseScreen(group) {
  selectedGroup.value = group;
  currentScreen.value = "expense";
}

function goToSummary(data) {
  summaryData.value = data;
  currentScreen.value = "summary";
}

function goBackToHome() {
  currentScreen.value = "home";
}

function goBackToExpense() {
  currentScreen.value = "expense";
}
</script>

<template>
  <div>
    <HomeComp
      v-if="currentScreen === 'home'"
      :groups="groups"
      @update-groups="groups = $event"
      @open-expenses="goToExpenseScreen"
    />

    <ExpenseComp
      v-if="currentScreen === 'expense'"
      :group="selectedGroup"
      @back="goBackToHome"
      @show-summary="goToSummary"
    />

    <SummaryComp
      v-if="currentScreen === 'summary'"
      :groupName="summaryData?.groupName"
      :members="summaryData?.members"
      @back="goBackToExpense"
    />
  </div>
</template>

<style scoped></style>
