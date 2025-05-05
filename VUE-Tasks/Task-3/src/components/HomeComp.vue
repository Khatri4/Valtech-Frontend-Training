<script setup>
import { ref } from "vue";

const props = defineProps({
  groups: Array,
});
const emit = defineEmits(["update-groups", "open-expenses"]);

const newGroup = ref("");
const newMember = ref("");
const groupIndex = ref(null);

function addGroup() {
  if (!newGroup.value) return alert("Enter group name");
  const exists = props.groups.some((g) => g.name === newGroup.value);
  if (exists) return alert("Group already exists");
  emit("update-groups", [
    ...props.groups,
    { name: newGroup.value, members: [] },
  ]);
  newGroup.value = "";
}

function removeGroup(index) {
  const newGroups = [...props.groups];
  newGroups.splice(index, 1);
  emit("update-groups", newGroups);
  groupIndex.value = null;
}

function selectedGroup(index) {
  groupIndex.value = index;
  newMember.value = "";
}

function addMember() {
  if (!newMember.value) return alert("Enter member name");
  const group = props.groups[groupIndex.value];
  if (group.members.includes(newMember.value)) {
    alert("Member already exists in this group");
    return;
  }
  const newGroups = [...props.groups];
  newGroups[groupIndex.value].members.push(newMember.value);
  emit("update-groups", newGroups);
  newMember.value = "";
}

function removeMember(gIdx, mIdx) {
  const newGroups = [...props.groups];
  newGroups[gIdx].members.splice(mIdx, 1);
  emit("update-groups", newGroups);
}

function openExpenses(idx) {
  emit("open-expenses", props.groups[idx]);
}
</script>

<template>
  <div>
    <h2>Create Group</h2>
    <input type="text" v-model="newGroup" />
    <button @click="addGroup">Create Group</button>

    <hr />
    <h2>Groups:</h2>
    <ol>
      <li v-for="(grp, idx) in groups" :key="idx">
        {{ grp.name }}
        <button @click="selectedGroup(idx)">Add Members</button>
        <button @click="removeGroup(idx)">Delete</button>
        <button @click="openExpenses(idx)">Expenses</button>

        <ul>
          <li v-for="(mem, midx) in grp.members" :key="midx">
            {{ mem }}
            <button @click="removeMember(idx, midx)">Remove</button>
          </li>
        </ul>
      </li>
    </ol>

    <div v-if="groupIndex !== null">
      <h3>Add members to {{ groups[groupIndex].name }}</h3>
      <input v-model="newMember" />
      <button @click="addMember">Add Member</button>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 16px;
}

input {
  margin-right: 8px;
  padding: 6px;
}

button {
  margin: 4px;
  padding: 6px 10px;
  cursor: pointer;
}

.group {
  border: 1px solid #ccc;
  padding: 12px;
  margin-top: 12px;
  border-radius: 4px;
}
</style>
