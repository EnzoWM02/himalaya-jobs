<script setup lang="ts">
const props = defineProps<{
  icon: string;
}>();
</script>
<template>
  <i class="icon material-symbols-outlined">
    {{ props.icon }}
  </i>
</template>
