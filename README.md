技術文件: Vue 2 Element-UI Table組件實現拖拽效果

概述： 本文介紹瞭如何在Vue 2和Element-UI中實現Table組件的拖拽效果。具體而言，我們將實現行拖拽和列拖拽兩種效果，分別使用Sortable.js庫來實現。

環境：

*   Vue.js v2.6.14
    
*   Element-UI v2.15.1 
    

*   在Vue組件中導入Element-UI和Sortable.js庫：
    

```
import Sortable from 'sortablejs'import { ElTable, ElTableColumn } from 'element-ui'export default {  name: 'DraggableTable',  components: {    ElTable,    ElTableColumn
  },  data() {    return {      //表格數據
      tableData: \[ /*...*/ \],      //表頭列數據
      dropCol: \[ /*...*/ \]
    }
  }
}
```

*   實現行拖拽效果：
    

*     
    

*   在Vue組件中導入Element-UI和Sortable.js庫：
    

```
import Sortable from 'sortablejs'import { ElTable, ElTableColumn } from 'element-ui'export default {  name: 'DraggableTable',  components: {    ElTable,    ElTableColumn
  },  data() {    return {      //表格數據
      tableData: \[ /*...*/ \],      //表頭列數據
      dropCol: \[ /*...*/ \]
    }
  }
}
```

*   實現行拖拽效果：
    
*   ```
//獲取表格tbody元素const tbody = document.querySelector('.el-table\_\_body-wrapper tbody')//使用Sortable.js庫實現行拖拽Sortable.create(tbody, {  onEnd({ newIndex, oldIndex }) {    const currRow = \_this.tableData.splice(oldIndex, 1)\[0\]
        _this.tableData.splice(newIndex, 0, currRow)
      }
    })
    ```
*   實現列拖拽效果：
    
*   ```
//獲取表頭tr元素const wrapperTr = document.querySelector('.el-table__header-wrapper tr')//使用Sortable.js庫實現列拖拽this.sortable = Sortable.create(wrapperTr, {
      onEnd: evt => {    const oldItem = this.dropCol\[evt.oldIndex\]    this.dropCol.splice(evt.oldIndex, 1)    this.dropCol.splice(evt.newIndex, 0, oldItem)
      }
    })
    ```
*   在Vue組件中使用Table組件，設置表格的列屬性和對應的表頭標籤：
    
*   ```
    sqlCopy code<el-table :data="tableData" border row-key="id" align="left">
      <el-table-column v-for="(item, index) in col" :key="\`col_${index}\`" :prop="dropCol\[index\].prop"
        :label="item.label">
      </el-table-column></el-table>
    ```
*   最後，可以在Vue組件的mounted()生命週期鈎子中調用行拖拽和列拖拽的方法，實現Table組件的拖拽效果：
    
```
mounted() {  this.rowDrop()  this.columnDrop()
    },methods: {  rowDrop() { /*...*/ },  columnDrop() { /*...*/ }
    }
    ```
*   總結： 本文通過介紹Vue 2和Element-UI中Table組件的拖拽效果的實現方法，具體實現步驟包括導入Sortable.js庫、獲取表格元素、設置行拖拽和列拖拽的回調函數等。
    
*   行拖拽實現步驟為：獲取表格的tbody元素 -> 使用Sortable.js庫實現拖拽效果 -> 實現onEnd回調函數，更新表格數據。
    
*   列拖拽實現步驟為：獲取表頭tr元素 -> 使用Sortable.js庫實現拖拽效果 -> 實現onEnd回調函數，更新表頭列數據。
    
*   最後，我們在Vue組件中使用Table組件並設置對應的列屬性和表頭標籤，並在mounted()生命週期鈎子中調用行拖拽和列拖拽的方法，實現Table組件的拖拽效果。
    
*   希望本文能夠對您實現Vue 2 Element-UI Table組件的拖拽效果有所幫助。

*   參考來源　https://www.cnblogs.com/jin-zhe/p/10181852.html[https://www.cnblogs.com/jin-zhe/p/10181852.html]