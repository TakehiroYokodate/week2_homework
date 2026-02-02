<script setup>
import ItemCard from './ItemCard.vue'

const props = defineProps({
  items: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['toggle-complete', 'delete-item'])

// ItemCardからのイベントをそのまま親(App.vue)にバケツリレーする
const handleToggle = (id) => emit('toggle-complete', id)
const handleDelete = (id) => emit('delete-item', id)
</script>

<template>
  <div class="item-list">
    <h3>買い物リスト</h3>
    <p v-if="items.length === 0" class="empty-msg">リストは空です。</p>

    <ItemCard
      v-for="item in items"
      :key="item.id"
      :item="item"
      @toggle-complete="handleToggle"
      @delete-item="handleDelete"
    />
  </div>
</template>

<style scoped>
.item-list {
  margin-top: 20px;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
}
.empty-msg {
  color: #888;
  font-style: italic;
}
</style>
