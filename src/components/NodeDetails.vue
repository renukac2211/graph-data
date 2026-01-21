<template>
  <div class="sidebar">
    <button class="close" @click="$emit('close')">✕</button>
    <h2>{{ node.name }}</h2>
    <p>{{ node.description }}</p>
  </div>
</template>

<script setup>
defineProps({
  node: Object
});
</script>

<style scoped>
.sidebar {
  flex: 1;
  padding: 20px;
  border-left: 1px solid #ddd;
  background: #fafafa;
}

.close {
  float: right;
  cursor: pointer;
  background: none;
  border: none;
  font-size: 18px;
}
</style>
