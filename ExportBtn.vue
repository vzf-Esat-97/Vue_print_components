/**
 * introduce : 导出Excel按钮
 * author    : cp
 * date      : 2019/04/29
 说明：项目中要安装插件 FileSaver和XLSX / npm install --save xlsx file-saver
 */
<template>
  <div class="export-btn">
    <el-button class="button"
               @click="exportExcel()">Excel导出</el-button>
    <div style="display:none;"
         class="tableDataAll">
      <table id="exportContent">
        <thead>
          <tr>
            <th>#</th>
            <th v-for="(item,idx) in thead_data"
                :key="idx">{{item[tabel_label]}}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item1,idx) in tbody_data"
              :key='idx'>
            <td>{{idx+1}}</td>
            <td v-for="(item,idx) in thead_data"
                :key="idx">
              <span v-if="item[special_field]">{{item1[special_field]}}</span>
              <span v-else>{{item1[item[tbody_name]]}}</span>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import FileSaver from 'file-saver'
import XLSX from 'xlsx'
export default {
  name: 'ExportBtn',
  props: {
    tbody_name: { // 表格名称
      type: String,
      default () {
        return ''
      }
    },
    tabel_label: { // 表头名称
      type: String,
      default () {
        return ''
      }
    },
    thead_data: { // 表头数据
      type: Array,
      default () {
        return []
      }
    },
    tbody_data: { // 表格数据
      type: Array,
      default () {
        return []
      }
    },
    special_field: { // 特殊显示字段
      type: String,
      default () {
        return ''
      }
    }
  },
  data () {
    return {
    }
  },
  mounted () {
  },
  methods: {
    exportExcel () {
      var wb = XLSX.utils.table_to_book(document.querySelector('#exportContent'))
      // #out - table需要导出表格的表单的id
      var wbout = XLSX.write(wb, { bookType: 'xlsx', bookSST: true, type: 'array' })
      try {
        FileSaver.saveAs(new Blob([wbout], { type: 'application/octet-stream' }), this.$route.meta.title + `.xlsx`)
      } catch (e) { if (typeof console !== 'undefined') console.log(e, wbout) }
      return wbout
    }
  }
}
</script>

<style lang="less">
</style>

<style lang="less" scoped>
.export-btn {
  margin-right: 10px;
  .tableDataAll {
    width: 100%;
    #exportContent {
      width: 100%;
      text-align: center;
      td {
        border: 1px solid;
      }
    }
  }
}
</style>
