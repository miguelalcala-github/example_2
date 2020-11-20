<template>
  <div class="showcase__container">
    <table>
      <tr>
        <th v-for="label in Object.keys(items[0])" :key="label">
          {{ label }}
        </th>
      </tr>
      <tr v-for="(item, index) in items" :key="index">
        <td v-for="label in Object.keys(item)" :key="label + index">
          <component :is="getComponent(label)" :data="item[label]" />
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
import RowBrewery from './RowBrewery'
import RowCountry from './RowCountry'
import RowData from './RowData'
import RowTags from './RowTags'

export default {
  components: {
    RowBrewery,
    RowCountry,
    RowData,
    RowTags,
  },

  props: {
    items: {
      type: Array,
      required: true,
    },
  },

  methods: {
    getComponent(label) {
      const dinamicComponents = ['tags', 'brewery', 'country']
      let component = 'row-data'
      console.log(label)
      if (dinamicComponents.includes(label)) {
        component = `row-${label}`
      }
      return component
    },
  },
}
</script>

<style scoped>
.showcase__container {
  margin-top: 2rem;
  padding: 3rem;
}
</style>
