<template>
  <div class="items-page">
    <div class="header-row">
      <div class="selected-items-block">
        <div v-if="selectedItems?.length > 0"
             class="items-block"
        >
          <div class="item-card"
               v-for="item in selectedItems"
               :key="item.id"
          >
            {{ item.name }}
          </div>
        </div>
        <div v-else
             class="items-block"
        >
          Корзина пуста
        </div>
      </div>
      <div class="selected-item-block">
        <div class="item-card" v-if="selectedItem">
          {{ selectedItem.name }}
        </div>
        <div v-else>
          Ничего не выбрано
        </div>
      </div>
    </div>

    <div class="lists-row">
      <div class="column">
        <div class="items-to-select"
             :class="{ 'selected-items': selectedItems?.includes(item) }"
             v-for="item in leftColumItems"
             :key="item.id"
             @click="handleSelectItems(item)"
        >
          {{ item.name }}
        </div>
      </div>
      <div class="column">
        <div class="item-to-select"
             :class="{ 'selected-item': item.id === selectedItem?.id }"
             v-for="item in rightColumItems"
             :key="item.id"
             @click="handleSelectItem(item)"
        >
          {{ item.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type {IShopItem} from "../models/IShopItem.ts";
import {ref} from "vue";

const leftColumItems: IShopItem[] = [
  {
    "id": 1,
    "name": "Shoes 1"
  },
  {
    "id": 2,
    "name": "Shoes 2"
  },
  {
    "id": 3,
    "name": "Shoes 3"
  },
  {
    "id": 4,
    "name": "Shoes 4"
  },
  {
    "id": 5,
    "name": "T-shirt 1"
  },
  {
    "id": 6,
    "name": "T-shirt 2"
  },
  {
    "id": 7,
    "name": "T-shirt 3"
  },
  {
    "id": 8,
    "name": "T-shirt 4"
  }
];

const rightColumItems: IShopItem[] = [
  {
    "id": 11,
    "name": "Jacket 1"
  },
  {
    "id": 12,
    "name": "Jacket 2"
  },
  {
    "id": 13,
    "name": "Jacket 3"
  },
  {
    "id": 14,
    "name": "Jacket 4"
  },
  {
    "id": 15,
    "name": "Hoodie 1"
  },
  {
    "id": 16,
    "name": "Hoodie 2"
  },
  {
    "id": 17,
    "name": "Hoodie 3"
  },
  {
    "id": 18,
    "name": "Hoodie 4"
  }
]

const selectedItems = ref<IShopItem[]>([]);
const selectedItem = ref<IShopItem | null>(null);

const handleSelectItems = (item: IShopItem) => {
  if (selectedItems?.value?.includes(item)) {
    return;
  }
  selectedItems?.value?.push(item);
};
const handleSelectItem = (item: IShopItem) => {
  selectedItem.value = item;
};
</script>

<style scoped>
.items-page {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.header-row {
  display: flex;
  justify-content: space-between;
  gap: 10px;
  padding: 10px 0;
}

.item-card {
  border: 1px solid black;
  padding: 10px;
}

.selected-items-block {
  width: 50%;
}
.items-block {
  border: 1px solid black;
  padding: 10px;
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}
.selected-item-block {
  border: 1px solid black;
  width: 50%;
  padding: 10px;
}
.selected-item-block .item-card {
  width: fit-content;
}

.lists-row {
  display: flex;
  justify-content: space-between;
  gap: 10px;
}
.column {
  border: 1px solid black;
  width: 50%;
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  padding: 10px;
}

.items-to-select {
  border: 1px solid black;
  padding: 10px;
}
.items-to-select:hover {
  cursor: pointer;
  background: green;
  color: white;
}
.selected-items {
  background: green;
  color: white;
}
.selected-items:hover {
  cursor: not-allowed;
}
.item-to-select {
  border: 1px solid black;
  padding: 10px;
}
.item-to-select:hover {
  cursor: pointer;
  background: orange;
}
.selected-item {
  background: orange;
}

</style>
