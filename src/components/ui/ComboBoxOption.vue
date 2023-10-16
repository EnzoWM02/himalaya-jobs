<script setup lang="ts">
import Icon from "./Icon.vue";

const props = defineProps<{
  value: string;
}>();
</script>

<template>
  <option :name="value">
    <slot />
  </option>
</template>
