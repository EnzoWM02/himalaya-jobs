<template>
  <select class="jobsListingOrder" name="jobsListingOrder">
    <slot />
  </select>
</template>

<style scoped>
.jobsListingOrder {
  border: 1px solid rgba(0, 0, 0, 0.3);
  border-radius: 8px;
  padding: 8px 12px;
  font-size: 14px;
}
</style>
