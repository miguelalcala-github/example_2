<template>
  <div>
    <table>
      <tr>
        <th v-for="countryLabel in Object.keys(data)" :key="countryLabel">
          {{ countryLabel }}
        </th>
      </tr>
      <tr>
        <td v-for="(info, index) in data" :key="index">
          {{ info }}
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      default: null,
    },
  },
}
</script>

<style scoped></style>
