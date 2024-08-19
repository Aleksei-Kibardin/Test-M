<template>
  <div class="container">
    <div class="top-section">
      <div class="selected-items">
        <div
          v-for="item in selectedItems"
          :key="item.id"
          class="item"
          @click="removeSelectedItem(item)"
        >
          {{ item.name }}
        </div>
        <div class="counter">selected: {{ selectedItems.length }} / 6</div>
      </div>
      <div class="selected-item" @click="selectedItem = null">
        <div v-if="selectedItem">{{ selectedItem.name }}</div>
      </div>
    </div>

    <div class="bottom-section">
      <div class="column">
        <div
          v-for="item in availableLeftItems"
          :key="item.id"
          class="item"
          @click="toggleSelectItem(item)"
        >
          {{ item.name }}
        </div>
      </div>
      <div class="column">
        <div
          v-for="item in availableRightItems"
          :key="item.id"
          class="item"
          @click="selectedItem = item"
        >
          {{ item.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const selectedItems = ref([]);
const selectedItem = ref(null);

const leftItems = ref([
  { id: 1, name: "Shoes 1" },
  { id: 2, name: "Shoes 2" },
  { id: 3, name: "Shoes 3" },
  { id: 4, name: "Shoes 4" },
  { id: 5, name: "T-shirt 1" },
  { id: 6, name: "T-shirt 2" },
  { id: 7, name: "T-shirt 3" },
  { id: 8, name: "T-shirt 4" },
]);

const rightItems = ref([
  { id: 11, name: "Jacket 1" },
  { id: 12, name: "Jacket 2" },
  { id: 13, name: "Jacket 3" },
  { id: 14, name: "Jacket 4" },
  { id: 15, name: "Hoodie 1" },
  { id: 16, name: "Hoodie 2" },
  { id: 17, name: "Hoodie 3" },
  { id: 18, name: "Hoodie 4" },
]);

// Доступные элементы для выбора слева (только невыбранные)
const availableLeftItems = computed(() => {
  return leftItems.value.filter((item) => !selectedItems.value.includes(item));
});

// Доступные элементы для выбора справа (если выбран, не показывается)
const availableRightItems = computed(() => {
  return rightItems.value.filter((item) => item !== selectedItem.value);
});

const toggleSelectItem = (item) => {
  if (selectedItems.value.length < 6 && !selectedItems.value.includes(item)) {
    selectedItems.value.push(item);
  }
};

const removeSelectedItem = (item) => {
  selectedItems.value = selectedItems.value.filter((i) => i.id !== item.id);
};
</script>

<style lang="scss">
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;

  .top-section {
    position: relative;
    display: flex;
    justify-content: space-between;
    width: 100%;
    max-width: 800px;
    margin-bottom: 20px;

    .selected-items {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      border: 2px solid black;
      gap: 10px;
      width: 300px;
      padding: 40px;
      user-select: none;
      .item {
        cursor: pointer;
        width: 60px;
        height: 60px;
        border: 2px solid black;
        display: flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 5px;
      }
    }

    .counter {
      position: absolute;
      bottom: 10px;
    }

    .selected-item {
      width: 200px;
      height: 200px;
      border: 2px solid black;
      display: flex;
      justify-content: center;
      align-items: center;
      user-select: none;
      cursor: pointer;
    }
  }

  .bottom-section {
    display: flex;
    gap: 20px;
    width: 100%;
    max-width: 800px;
    user-select: none;
    .column {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      border: 2px solid black;
      padding: 10px;
      flex: 1;

      .item {
        width: 60px;
        height: 60px;
        border: 2px solid black;
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
        &:hover {
          background-color: lightgrey;
        }
      }
    }
  }
}
</style>
