<template>
  <div>
    <span v-for="tag in data" :key="tag">{{ tag }}</span>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Array,
      default: null,
    },
  },
}
</script>

<style scoped></style>
