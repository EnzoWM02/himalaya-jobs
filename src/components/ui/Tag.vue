<script setup lang="ts">
defineProps<{
  text: string;
  color: string;
  backgroundColor: string;
  dot?: boolean;
}>();
</script>

<template>
  <div class="tagWrapper">
    <div v-if="dot" class="dot" />
    <span class="tagText"> {{ text }} </span>
  </div>
</template>

<style scoped>
.tagWrapper {
  padding: 1px 8px;
  border-radius: 18px;
  background-color: v-bind(backgroundColor);
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 4px;
}
.tagText {
  font-size: 11px;
  font-weight: 600;
  color: v-bind(color);
}
.dot {
  width: 5px;
  height: 5px;
  border-radius: 100%;
  background-color: v-bind(color);
}
</style>
