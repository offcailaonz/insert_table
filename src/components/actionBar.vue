<template>
  <v-row>
    <v-col cols="6" style="display: flex;">
      <v-text-field
        outlined
        placeholder="Material"
        hide-details
        dense
      ></v-text-field>
      <!-- <v-btn>Search</v-btn> -->
      <v-btn @click="search" style="margin-left: 8px;">
        <v-icon left>
          mdi-file-find
        </v-icon>
        Search
      </v-btn>
    </v-col>
    <v-col cols="6" align="end">
      <v-btn @click="add">
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
  props: {
  },
  methods: {
    search() {
      this.$emit('search')
    },
    add() {
      this.$emit('add')
    },
    insert() {
      this.$emit('insert')
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
  