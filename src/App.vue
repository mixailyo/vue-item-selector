<template>
  <div class="container">
    <div class="top">
      <div class="top-left">
        <div class="items">
          <div v-for="item in selectedUserItems" :key="item.id" class="item">
            {{ item.name }}
          </div>
        </div>
        <div class="counter">selected: {{ selectedUserItems.length }} / {{ maxSelectedItems }}</div>
      </div>
      <div class="top-right">
        <div v-if="selectedOptionItem" class="item">
          {{ selectedOptionItem.name }}
        </div>
      </div>
    </div>
    <div class="bottom">
      <div class="left">
        <div 
          v-for="item in userItems" 
          :key="item.id"
          class="item" 
          :class="{'selected': isUserItemSelected(item)}"
          @click="toggleUserItem(item)"
        >
          {{ item.name }}
        </div>
      </div>
      <div class="right">
        <div 
          v-for="item in optionItems" 
          :key="item.id"
          class="item"  
          :class="{'selected': isOptionItemSelected(item)}"
          @click="selectOptionItem(item)"
        >
          {{ item.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

interface Item {
  id: number;
  name: string;
}

const maxSelectedItems = 6;

const userItems = ref<Item[]>([
  { id: 1, name: 'Shoes 1' },
  { id: 2, name: 'Shoes 2' },
  { id: 3, name: 'Shoes 3' },
  { id: 4, name: 'Shoes 4' },
  { id: 5, name: 'T-shirt 1' },
  { id: 6, name: 'T-shirt 2' },
  { id: 7, name: 'T-shirt 3' },
  { id: 8, name: 'T-shirt 4' },
]);

const optionItems = ref<Item[]>([
  { id: 11, name: 'Jacket 1' },
  { id: 12, name: 'Jacket 2' },
  { id: 13, name: 'Jacket 3' },
  { id: 14, name: 'Jacket 4' },
  { id: 15, name: 'Hoodie 1' },
  { id: 16, name: 'Hoodie 2' },
  { id: 17, name: 'Hoodie 3' },
  { id: 18, name: 'Hoodie 4' },
]);

const selectedUserItems = ref<Item[]>([]);
const selectedOptionItem = ref<Item | null>(null);

const isUserItemSelected = (item: Item): boolean => {
  return selectedUserItems.value.includes(item);
};

const isOptionItemSelected = (item: Item): boolean => {
  return selectedOptionItem.value?.id === item.id;
};

const toggleUserItem = (item: Item) => {
  if (selectedUserItems.value.includes(item)) {
    selectedUserItems.value = selectedUserItems.value.filter(i => i.id !== item.id);
  } else if (selectedUserItems.value.length < maxSelectedItems) {
    selectedUserItems.value.push(item);
  }
};

const selectOptionItem = (item: Item) => {
  selectedOptionItem.value = item;
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.top {
  display: flex;
  justify-content: space-between;
  width: 100%;
  max-width: 800px;
}

.top-left, .top-right {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 10px;
  border: 2px solid black;
  width: 48%;
  min-height: 100px;
}

.bottom {
  display: flex;
  justify-content: space-between;
  width: 100%;
  max-width: 800px;
}

.left, .right {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  padding: 10px;
  border: 2px solid black;
  width: 48%;
}

.items {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 20px;
}

.item {
  padding: 10px;
  border: 1px solid black;
  cursor: pointer;
  text-align: center;
  min-width: 60px;
}

.selected {
  background-color: lightgreen;
}

.counter {
  margin-top: auto;
}
</style>