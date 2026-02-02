<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add-item'])

// フォームの入力値を保持するリアクティブ変数
const name = ref('')
const quantity = ref(1)

const handleSubmit = () => {
  // バリデーション: 商品名が空なら何もしない
  if (!name.value.trim()) return

  // 親にデータを渡す
  emit('add-item', {
    name: name.value,
    quantity: quantity.value
  })

  // フォームをリセット
  name.value = ''
  quantity.value = 1
}
</script>

<template>
  <div class="input-container">
    <input 
      v-model="name" 
      type="text" 
      placeholder="商品名を入力" 
      class="input-field"
    />
    <input 
      v-model="quantity" 
      type="number" 
      min="1" 
      class="input-quantity"
    />
    <button @click="handleSubmit" class="add-btn">追加</button>
  </div>
</template>

<style scoped>
.input-container {
  display: flex;
  gap: 10px;
  padding: 20px;
  background-color: #e6f7ff;
  border-radius: 8px;
  margin-bottom: 20px;
}

.input-field {
  flex-grow: 1;
  padding: 8px;
}

.input-quantity {
  width: 60px;
  padding: 8px;
}

.add-btn {
  background-color: #1890ff;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
}

.add-btn:hover {
  background-color: #40a9ff;
}
</style>
