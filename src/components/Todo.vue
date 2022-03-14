<script setup>
import { ref } from "vue";

const com = "#ccffcc";
const unCom = "#ffcccc";
let i = 1;
const itemName = ref("");
let items = ref([

]);

function addItem(e) {
  if (itemName.value !== "") {
    items.value.push({
      title: itemName.value,
      color: unCom,
      complete: false,
      index: i,
      checked: "",
    });
    i++;
    itemName.value = "";
  }
}

function deleteItem(itemIndex) {
  items.value = items.value.filter((item) => item.index != itemIndex);

  console.log("delete " + itemIndex);
}

function markAsDone(itemIndex) {
  items.value.map((item) => {
    if (item.index === itemIndex) {
      item.complete = !item.complete;
      item.color = item.complete ? com : unCom;
    }
    return item;
  });
}
</script>

<template>
  <h1>Petters Vue Todo list</h1>

  <div>
    <input v-model="itemName" />
    <input type="button" @click="addItem" value="Lägg till" />
  </div>

  <span>
    <div v-for="(item, index) in items" :key="index">
      <div :style="{ backgroundColor: item.color }" :id="index">
        <input
          type="checkbox"
          @click="markAsDone(item.index)"
          v-model="item.checked"
        />
        {{ item.title }}
        <input
          type="button"
          @click="deleteItem(item.index)"
          value="Ta bort"
        />
      </div>
    </div>
  </span>
</template>

<style>
div {
  padding: 8px;
}
</style>
