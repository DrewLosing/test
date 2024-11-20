<template>
  <div class="container">
    <!-- Верхние блоки -->
    <div class="top-blocks">
      <div class="selected-items">
        <h3>Selected Items</h3>
        <div class="items">
          <div v-for="item in selectedUserItems" :key="item.id" class="item">
            {{ item.name }}
          </div>
        </div>
        <p>Selected: {{ selectedUserItems.length }} / 6</p>
      </div>
      <div class="selected-item">
        <h3>Selected Item</h3>
        <div class="item" v-if="selectedChoiceItem">
          {{ selectedChoiceItem ? selectedChoiceItem.name : "None" }}
        </div>
      </div>
    </div>

    <!-- Нижние блоки -->
    <div class="bottom-blocks">
      <div class="user-items">
        <h3>User Items</h3>
        <div class="items">
          <div
              v-for="item in userItems"
              :key="item.id"
              :class="{ selected: selectedUserItems.includes(item) }"
              class="item"
              @click="toggleUserItem(item)"
          >
            {{ item.name }}
          </div>
        </div>
      </div>
      <div class="choice-items">
        <h3>Choice Items</h3>
        <div class="items">
          <div
              v-for="item in choiceItems"
              :key="item.id"
              :class="{ selected: selectedChoiceItem && selectedChoiceItem.id === item.id }"
              class="item"
              @click="selectChoiceItem(item)"
          >
            {{ item.name }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    // Коллекции данных
    const userItems = ref([
      { id: 1, name: "Shoes 1" },
      { id: 2, name: "Shoes 2" },
      { id: 3, name: "Shoes 3" },
      { id: 4, name: "Shoes 4" },
      { id: 5, name: "T-shirt 1" },
      { id: 6, name: "T-shirt 2" },
      { id: 7, name: "T-shirt 3" },
      { id: 8, name: "T-shirt 4" },
    ]);

    const choiceItems = ref([
      { id: 11, name: "Jacket 1" },
      { id: 12, name: "Jacket 2" },
      { id: 13, name: "Jacket 3" },
      { id: 14, name: "Jacket 4" },
      { id: 15, name: "Hoodie 1" },
      { id: 16, name: "Hoodie 2" },
      { id: 17, name: "Hoodie 3" },
      { id: 18, name: "Hoodie 4" },
    ]);

    // Состояние выбора
    const selectedUserItems = ref([]);
    const selectedChoiceItem = ref(null);

    // Логика выбора вещей из пользовательского списка
    const toggleUserItem = (item) => {
      if (selectedUserItems.value.includes(item)) {
        selectedUserItems.value = selectedUserItems.value.filter(
            (i) => i.id !== item.id
        );
      } else if (selectedUserItems.value.length < 6) {
        selectedUserItems.value.push(item);
      }
    };

    // Логика выбора одной вещи из общего списка
    const selectChoiceItem = (item) => {
      selectedChoiceItem.value = item;
    };

    return {
      userItems,
      choiceItems,
      selectedUserItems,
      selectedChoiceItem,
      toggleUserItem,
      selectChoiceItem,
    };
  },
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.top-blocks {
  display: flex;
  justify-content: space-between;
}

.bottom-blocks {
  display: flex;
  justify-content: space-between;
}

.selected-items,
.selected-item,
.user-items,
.choice-items {
  border: 1px solid black;
  padding: 10px;
  width: 45%;
}

.items {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.item {
  border: 1px solid gray;
  padding: 5px 10px;
  cursor: pointer;
  width: fit-content;
}

.item.selected {
  background-color: lightblue;
  border-color: blue;
}
</style>
