<!-- eslint-disable vue/valid-v-slot -->
<template>
  <table ref="myTable">
    <tr>
      <th v-for="(head, indexHead) in headers" :key="indexHead" > {{ head.text }}</th>
    </tr>
    <tr v-for="(item, indexItem) in items" :key="indexItem">
      <td v-for="(value, indexValue) in headers" :key="indexValue" style="padding-left: 20px; padding-right: 20px;">
        <span v-if="(indexValue === 0)">
          {{ item[value.value] }}
        </span>
        <span v-else-if="(indexValue+1 === headers.length)">
          {{ summaryQTY(item) }}
        </span>
        <div v-else>
          <input
            type="number"
            :tabindex="(indexItem + indexValue * items.length) - (items.length - 1)"
            v-model="item[value.value].QTY"
            >
        </div>
      </td>
    </tr>
  </table>
</template>


<script>

export default {
  name: 'InsertTable',
  props: {
    headers: {
      type: Array,
      default: null,
    },
    items: {
      type: Array,
      default: null,
    },
  },
  data() {
    return {
      password: 'asd'
    };
  },
  methods: {
    summaryQTY(item) {
      let totalQty = 0
      for (const key in item) {
        if (key !== "Material") {
          totalQty += Number(item[key].QTY) || 0;
        }
      }
      return totalQty
    },
    insertData(value) {
      console.log(value)
    },
  },
}
</script>

<style scoped>
.spacing-card {
  margin-top: 24px;
  margin-bottom: 24px;
}

table {
  width: 100%;
  margin-top: 12px;
}

th, td {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

th {
  background-color: #1976d2;
  color: white;
  text-align: center;
}

tr:nth-child(2n+1) {
  background-color: #cfe7ff;
}

input {
  width: 100%;
  padding: 6px;
  box-sizing: border-box;
  border: 1px solid #dddddd;
}

</style>
  