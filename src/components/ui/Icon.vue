<script setup lang="ts">
const props = defineProps<{
  icon: string;
}>();
</script>
<template>
  <span class="icon material-symbols-outlined">
    {{ props.icon }}
  </span>
</template>
