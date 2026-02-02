<script setup>
import { ref } from 'vue'
import ItemInput from './components/ItemInput.vue'
import ItemList from './components/ItemList.vue'

// 商品データの配列を管理
const items = ref([
  { id: 1, name: 'りんご', quantity: 3, completed: false }
])

// 商品の追加ロジック
const addItem = (payload) => {
  items.value.push({
    id: Date.now(), // ユニークなIDとして現在時刻を使用
    name: payload.name,
    quantity: payload.quantity,
    completed: false
  })
}

// 完了状態の切り替えロジック
const toggleComplete = (id) => {
  const item = items.value.find(i => i.id === id)
  if (item) {
    item.completed = !item.completed
  }
}

// 商品の削除ロジック
const deleteItem = (id) => {
  items.value = items.value.filter(i => i.id !== id)
}
</script>

<template>
  <div class="app-container">
    <h1>お買い物リスト</h1>
    
    <ItemInput @add-item="addItem" />

    <ItemList 
      :items="items" 
      @toggle-complete="toggleComplete" 
      @delete-item="deleteItem" 
    />
  </div>
</template>

<style scoped>
.app-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: sans-serif;
}

h1 {
  text-align: center;
  color: #333;
}
</style>
