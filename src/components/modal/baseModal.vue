<template>
  <v-row justify="center">
    <v-dialog
      v-model="dialog"
      persistent
      max-width="400"
    >
      <v-card>
        <v-card-title class="text-h5">
          Add Material
        </v-card-title>
        <v-card-text>
          <form ref="form">
            <v-row>
              <v-col cols="4" align="start" class="align-self-center">
                <div class="black--text" >Material :</div>
              </v-col>
              <v-col cols="8" align="end">
                <v-text-field
                  :rules="rulesRequired"
                  v-model="form.material"
                  label="Material"
                  required
                  outlined
                  dense
                  hide-details
                ></v-text-field>
              </v-col>
              <v-col cols="4" align="start" class="align-self-center">
                <div class="black--text" >Product Code :</div>
              </v-col>
              <v-col cols="8" align="end">
                <v-text-field
                  :rules="rulesRequired"
                  v-model="form.productCode"
                  label="Product Code"
                  required
                  outlined
                  dense
                  hide-details
                ></v-text-field>
              </v-col>
              <v-col cols="4" align="start" class="align-self-center">
                <div class="black--text" >Description :</div>
              </v-col>
              <v-col cols="8" align="end">
                <v-text-field
                  v-model="form.description"
                  label="Description"
                  outlined
                  dense
                  hide-details
                ></v-text-field>
              </v-col>
            </v-row>
            <div class="d-flex justify-space-between mt-4">
              <v-btn
                class="mr-4"
                @click="cancel()"
                color="error"
                >
                cancel
              </v-btn>
              <v-btn @click="save" :disabled="!form.material.length && !form.productCode.length" color="primary">
                ADD
              </v-btn>
            </div>
          </form>
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>

export default {
  name: 'TitleBar',
  data () {
    return {
      dialog: false,
      rulesRequired: [
        v => !!v || 'required',
        v => /^[a-zA-Z0-9]+$/.test(v) || 'must be in English or a number',
      ],
      form: {
        material: '',
        productCode: '',
        description: ''
      }
    }
  },
  methods: {
    save () {
      console.log('save')
      this.$emit('add', this.form)
      this.dialog = false
      this.form = {
        material: '',
        productCode: '',
        description: ''
      }
    },
    cancel () {
      this.dialog = false
      this.form = {
        material: '',
        productCode: '',
        description: ''
      }
    }
  }
}
</script>

<style scoped>
</style>ƒ
  