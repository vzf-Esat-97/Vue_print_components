/**
 * introduce : 打印功能按钮
 * author    : cp
 * date      : 2019/04/28
 说明：项目中要安装插件 print-js / npm install print-js --save
 */
<template>
  <div class="maths-btn">
    <el-button class="button"
               @click="buttonAddUser()">打 印</el-button>
    <div style="display:none;"
         class="tableDataAll">
      <table id="printContent">
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
import printJS from 'print-js'
export default {
  name: 'PrintBtn',
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
    thead_data: { // 表格表头
      type: Array,
      default () {
        return []
      }
    },
    tbody_data: { // 表格内容
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
    buttonAddUser () {
      console.log('打印')
      const style = '@page {width:100%} @media print {h1 { color: blue }} table{width:100%;font-size:24px;text-align:center;border-collapse:collapse;}th{padding:10px; height:40px; border:1px solid #EBEEF5;} td{height:40px; font-size:14px; color:#606266; line-height: 40px; border:1px solid #EBEEF5;}'// 自定义样式
      printJS({
        printable: 'printContent',
        type: 'html',
        style: style,
        scanStyles: false
      })
    }
  }
}
</script>

<style lang="less">
</style>

<style lang="less" scoped>
.maths-btn {
  margin-right: 10px;
  .tableDataAll {
    width: 100%;
    #printContent {
      width: 100%;
      text-align: center;
      td {
        border: 1px solid;
      }
    }
  }
}
</style>
