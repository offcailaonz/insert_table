<template>
  <v-card class="spacing-card">
    <v-row>
      <v-col cols="6" align="start">
        <v-card-title style="padding: 0px; height: 36px;">
          INSERT STOCK TABLE
        </v-card-title>
      </v-col>
      <v-col cols="6" align="end">
        <v-btn @click="save" color="green" class="white--text">
          <v-icon left>
            mdi-content-save-all
          </v-icon>
          SAVE
        </v-btn>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>

export default {
  name: 'TitleBar',
  methods: {
    save () {
      this.$emit('save')
    }
  }
}
</script>

<style scoped>
.spacing-card {
  margin-top: 24px;
  margin-bottom: 12px;
  padding: 12px;
  display: flex;
}
</style>ƒ
  