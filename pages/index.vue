<template>
  <div class="container">
    <Header />
    <div class="selection">
      <label for="max-beer">Beers to show: </label>
      <input id="max-beer" v-model="maxItems" type="number" name="max-beer" />
    </div>
    <p v-if="$fetchState.pending">Fetching Beers...</p>
    <p v-else-if="$fetchState.error">An error occurred :(</p>

    <Showcase v-else :items="items" />
    <button class="btn" @click="refresh()">Refresh</button>
  </div>
</template>

<script>
export default {
  fetchOnServer: false,
  async fetch() {
    try {
      while (this.items.length < this.maxItems) {
        const newItem = await fetch(
          'http://cors-anywhere.herokuapp.com/http://prost.herokuapp.com/api/v1/beer/rand'
        )
          .then((response) => {
            if (response.status === 200) {
              return response.json()
            } else {
              throw new Error('failed to fetch')
            }
          })
          .then((data) => {
            if (this.items.includes(data)) {
              this.$fetch()
            } else {
              return data
            }
          })
          .catch((e) => {
            throw new Error(e.message)
          })
        console.log(newItem)
        this.items.push(newItem)
      }
    } catch (e) {
      throw new Error(e.message)
    }
  },
  watch: {
    maxItems: '$fetch',
  },
  data() {
    return {
      items: [],
      maxItems: 2,
      error: '',
    }
  },
  methods: {
    refresh() {
      this.items = []
      this.$fetch()
    },
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  text-align: center;
}
.selection {
  margin-top: 2rem;
}

.selection label {
  display: block;
}

.selection input {
  margin-top: 1rem;
}
.btn {
  align-self: center;
  margin: 3rem;
  padding: 0.25rem 0.75rem;
}
.links {
  padding-top: 15px;
}
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}
td,
th {
  text-align: left;
  padding: 8px;
}
td td,
td th {
  border: 1px dotted #808080;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
</style>
