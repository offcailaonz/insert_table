<template>
  <div class="pt-10">
    <BaseModal ref="modalAddMaterial" @add="createMaterial"/>
    <TitleBar @save="saveTable"/>
    <v-card class="pa-3">
      <ActionBar
        @search="searchData"
        @add="addMaterial"
        />
      <InsertTable
        :headers="headerTable"
        :items="filterData"
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
      filter: '',
      maxID: 0,
      uniqueLocations: [],
      mockUpDataOnGetApi: [
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
  computed: {
    filterData() {
      return this.filter ? this.itemsTable.filter(item => item.Material.includes(this.filter)) : this.itemsTable
    }
  },
  methods: {
    async getData() {
      try {
        console.log('GET DATA')
        this.rawData = await [...this.mockUpDataOnGetApi]
        this.mapDataTable()
      } catch (error) {
        console.log('error', error)
      }
    },
    mapDataTable() {
      if (this.rawData.length) {
        this.uniqueLocations = [...new Set(this.rawData.map(item => item.Location).sort())]
        const headers = this.uniqueLocations.map((header) => {
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
          this.uniqueLocations.forEach((location) => {
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
    },
    saveTable() {
      const data = this.itemsTable
      const dataSaveTable = []
      const dataNoIDSaveTable = []

      data.forEach((item) => {
        this.uniqueLocations.forEach((location) => {
          if (item[location] && item[location].QTY > 0) {
            if (!item[location].ID) {
              item[location].Location = location
              dataNoIDSaveTable.push(item[location])
            } else {
              dataSaveTable.push(item[location])
            }
          }
        })
      })
      let idMax = dataSaveTable.sort((a, b) => a.ID - b.ID)[dataSaveTable.length - 1].ID
      dataNoIDSaveTable.forEach((data) => {
        idMax = idMax + 1
        data.ID = idMax
      })
      const finalDataSaveTable = [...dataSaveTable, ...dataNoIDSaveTable]
      this.rawData = [...finalDataSaveTable]
      console.log('finalDataSaveTable', finalDataSaveTable)
    },
    searchData(value) {
      this.filter = value
    },
    addMaterial() {
      this.$refs.modalAddMaterial.dialog = !this.$refs.modalAddMaterial.dialog
    },
    async createMaterial(form) {
      const item = {
        Material: form.material,
        ProductCode: form.productCode,
        Location: this.mockUpDataOnGetApi[0].Location
      }
      this.uniqueLocations.forEach((location) => {
        if (!Object.keys(item).includes(location)) {
          item[location] = {
            ID: null,
            Material: item.Material,
            ProductCode: item.ProductCode,
            Location: location,
            QTY: 0
          }
        }
      })
      this.itemsTable.push(item)
    },
  }
}

</script>

<style scoped>
</style>
  