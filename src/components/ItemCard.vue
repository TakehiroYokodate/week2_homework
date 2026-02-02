<script setup>
// Propsの定義: 親から商品データを受け取る
const props = defineProps({
  item: {
    type: Object,
    required: true
  }
})

// Emitsの定義: 親へイベントを通知する
const emit = defineEmits(['toggle-complete', 'delete-item'])
</script>

<template>
  <div class="item-card" :class="{ completed: item.completed }">
    <div class="info">
      <input 
        type="checkbox" 
        :checked="item.completed" 
        @change="emit('toggle-complete', item.id)"
      >
      <span class="name">{{ item.name }}</span>
      <span class="quantity">数量: {{ item.quantity }}</span>
    </div>
    
    <button class="delete-btn" @click="emit('delete-item', item.id)">削除</button>
  </div>
</template>

<style scoped>
.item-card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #ddd;
  padding: 10px;
  margin-bottom: 8px;
  border-radius: 4px;
  background-color: #fff;
}

.info {
  display: flex;
  align-items: center;
  gap: 10px;
}

/* 完了した商品は視覚的に区別（取り消し線と色変更） */
.completed .name,
.completed .quantity {
  text-decoration: line-through;
  color: #888;
}

.delete-btn {
  background-color: #ff4d4f;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
}

.delete-btn:hover {
  background-color: #d9363e;
}
</style>
