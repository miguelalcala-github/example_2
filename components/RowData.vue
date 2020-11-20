<template>
  <div>
    <span>{{ data }}</span>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: String,
      default: () => '',
    },
  },
}
</script>

<style scoped></style>
