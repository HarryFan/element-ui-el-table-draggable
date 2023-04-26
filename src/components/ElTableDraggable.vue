<template>
  <div style="width:800px">

    <el-table :data="tableData" border row-key="id" align="left">
      <el-table-column v-for="(item, index) in col" :key="`col_${index}`" :prop="dropCol[index].prop"
        :label="item.label">
      </el-table-column>
    </el-table>
    <pre style="text-align: left">
      {{dropCol}}
    </pre>
    <hr>
    <pre style="text-align: left">
      {{tableData}}
    </pre>
  </div>
</template>

<script>
  import Sortable from 'sortablejs'

  export default {
    name: 'HelloWorld',
    props: {
      msg: String
    },
    components: {

    },

    data() {
      return {
        col: [{
            label: '日期',
            prop: 'date'
          },
          {
            label: '姓名',
            prop: 'name'
          },
          {
            label: '地址',
            prop: 'address'
          }
        ],
        dropCol: [{
            label: '日期',
            prop: 'date'
          },
          {
            label: '姓名',
            prop: 'name'
          },
          {
            label: '地址',
            prop: 'address'
          }
        ],
        tableData: [
          {
            id: '1',
            date: '2023-01-02',
            name: '林小明1',
            address: '台北市大安區通化街 100 巷'
          },
          {
            id: '2',
            date: '2023-01-04',
            name: '林小明2',
            address: '台北市大安區通化街 200 巷'
          },
          {
            id: '3',
            date: '2023-01-01',
            name: '林小明3',
            address: '台北市大安區通化街 300 巷'
          },
          {
            id: '4',
            date: '2023-01-03',
            name: '林小明4',
            address: '台北市大安區通化街 400 巷'
          }
        ]
      }
    },
    mounted() {
      this.rowDrop() // 行拖拽
      this.columnDrop() // 列拖拽
    },
    methods: {
      // 行拖拽
      rowDrop() {
        const tbody = document.querySelector('.el-table__body-wrapper tbody')
        const _this = this
        Sortable.create(tbody, {
          onEnd({
            newIndex,
            oldIndex
          }) {
            const currRow = _this.tableData.splice(oldIndex, 1)[0]
            _this.tableData.splice(newIndex, 0, currRow)
          }
        })
      },
      // 列拖拽
      columnDrop() {
        const wrapperTr = document.querySelector('.el-table__header-wrapper tr')
        this.sortable = Sortable.create(wrapperTr, {
          animation: 180,
          delay: 0,
          onEnd: evt => {
            const oldItem = this.dropCol[evt.oldIndex]
            this.dropCol.splice(evt.oldIndex, 1)
            this.dropCol.splice(evt.newIndex, 0, oldItem)
          }
        })
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
