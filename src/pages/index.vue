<template>
  <div class="pt-10">
    <BaseModal ref="modalAddMaterial"/>
    <TitleBar @save="saveTable"/>
    <v-card class="pa-3">
      <ActionBar
        @search="searchData"
        @add="addData"
        />
      <InsertTable
        :headers="headerTable"
        :items="itemsTable"
      />
    </v-card>
  </div>
</template>

<script>
import TitleBar from '../components/titleBar.vue'
import ActionBar from '../components/actionBar.vue'
import InsertTable from '../components/insertTable.vue'
import BaseModal from '../components/modal/baseModal.vue'

export default {
  name: 'HomePage',
  components: {
    TitleBar,
    ActionBar,
    BaseModal,
    InsertTable
  },
  data () {
    return {
      rawData: [],
      headerTable: [],
      itemsTable: [],
      is_insert: true,
      mockUpData: [
        {
          ID: 1,
          Material: "MAT0001",
          ProductCode: "PC000001",
          Location: "A1",
          QTY: 100
        },
        {
          ID: 2,
          Material: "MAT0001",
          ProductCode: "PC000001",
          Location: "A2",
          QTY: 100
        },
        {
          ID: 3,
          Material: "MAT0001",
          ProductCode: "PC000001",
          Location: "A4",
          QTY: 100
        },
        {
          ID: 4,
          Material: "MAT0002",
          ProductCode: "PC000002",
          Location: "A1",
          QTY: 100
        },
        {
          ID: 5,
          Material: "MAT0002",
          ProductCode: "PC000002",
          Location: "A3",
          QTY: 100
        },
        {
          ID: 6,
          Material: "MAT0003",
          ProductCode: "PC000003",
          Location: "A1",
          QTY: 100
        },
        {
          ID: 7,
          Material: "MAT0004",
          ProductCode: "PC000004",
          Location: "A2",
          QTY: 100
        }
      ]
    }
  },
  mounted () {
    this.$nextTick(() => {
      this.getData()
    })
  },
  methods: {
    getData() {
      try {
        console.log('GET DATA')
        this.rawData = [...this.mockUpData]
        
        if (this.rawData.length) {
          const uniqueLocations = [...new Set(this.rawData.map(item => item.Location).sort())]
          const headers = uniqueLocations.map((header) => {
            return { text: header, value: header }
          })
          this.headerTable = [
            { text: 'Material', value: 'Material' },
            ...headers,
            { text: 'Sum', value: 'Sum' },
          ]
          
          const result = this.rawData.reduce((acc, item) => {
            const Material = item.Material
            const Location = item.Location
            if (!acc[Material]) {
              acc[Material] = acc[Material] = {
                "Material": Material,
                "ProductCode": item.ProductCode,
                "Location": item.Location
              };
            }
            acc[Material][Location] = item;
            return acc;
          }, {});
          const Result = Object.values(result);
          Result.forEach((item) => {
            uniqueLocations.forEach((location) => {
              if (!Object.keys(item).includes(location)) {
                item[location] = {
                    ID: null,
                    Material: item.Material,
                    ProductCode: item.ProductCode,
                    Location: item.Location,
                    QTY: 0
                }
              }
            })
          })
          this.itemsTable = Result
        }

      } catch (error) {
        console.log('error', error)
      }
    },
    saveTable() {
      console.log('saveTable', this.itemsTable)
    },
    searchData() {
      console.log('searchData')
    },
    addData() {
      this.$refs.modalAddMaterial.dialog = !this.$refs.modalAddMaterial.dialog
      console.log('addData', this.$refs.modalAddMaterial.dialog)
    },
  }
}

</script>

<style scoped>
</style>
  