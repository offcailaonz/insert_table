<template>
  <v-row>
    <v-col cols="6" style="display: flex;">
      <v-text-field
        v-model="valueSearch"
        outlined
        placeholder="Material"
        hide-details
        dense
      ></v-text-field>
      <!-- <v-btn>Search</v-btn> -->
      <v-btn @click="search" style="margin-left: 8px;" color="secondary">
        <v-icon left>
          mdi-file-find
        </v-icon>
        Search
      </v-btn>
    </v-col>
    <v-col cols="6" align="end">
      <v-btn @click="add" color="primary">
        <v-icon left>
          mdi-plus
        </v-icon>
        ADD Material
      </v-btn>
    </v-col>
  </v-row>
</template>

<script>

export default {
  name: 'ActionBar',
  data () {
    return {
      valueSearch: ''
    }
  },
  props: {
  },
  watch: {
    valueSearch (newVal) {
      if (!newVal.length) {
        this.search()
      }
    }
  },
  methods: {
    search() {
      this.$emit('search', this.valueSearch)
    },
    add() {
      this.$emit('add')
    }
  }
}
</script>

<style scoped>
.card {
  margin-top: 24px;
  margin-bottom: 0px;
  padding: 16px;
}
</style>ƒ
  