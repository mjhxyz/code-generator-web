<template>
  <div class="app-container">
    <el-dialog
      title="添加"
      :visible.sync="showAdd"
      width="800px"
      :close-on-click-modal="false"
    >
      <!-- 添加信息弹出框 -->
      <el-form
        ref="addform"
        :model="addForm"
        label-width="80px"
        :rules="tableRules"
      >
        <el-form-item
          v-for="field in addibleFields"
          :key="field.name"
          :label="field.label"
          :prop="field.name"
        >
          <el-date-picker
            v-if="field.type === 'datetime'"
            v-model="addForm[field.name]"
            type="datetime"
            value-format="yyyy-MM-dd HH:mm:ss"
            :placeholder="field.placeholder || '选择日期时间'"
          />
          <el-select
            v-else-if="Array.isArray(field.type)"
            v-model="addForm[field.name]"
            :placeholder="field.placeholder"
          >
            <el-option
              v-for="item in field.type"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            />
          </el-select>
          <el-input
            v-else
            v-model="addForm[field.name]"
            :placeholder="field.placeholder"
          />
        </el-form-item>
      </el-form>
      <span
        slot="footer"
        class="dialog-footer"
      >
        <el-button
          type="success"
          @click="addSubmit"
        >提 交</el-button>
        <el-button
          type="danger"
          @click="showAdd = false"
        >关 闭</el-button>
      </span>
    </el-dialog>
    <div class="app-header">
      <el-button
        size="small"
        type="primary"
        icon="el-icon-plus"
      >新增</el-button>
      <el-button
        size="small"
        type="warning"
        icon="el-icon-edit"
      >修改</el-button>
      <el-button
        size="small"
        type="danger"
        icon="el-icon-delete"
      >删除</el-button>
      <el-button
        size="small"
        type="success"
        icon="el-icon-info"
      >详情</el-button>
    </div>
    <el-table
      class="app-body"
      :data="table.list"
      element-loading-text="加载中..."
      border
      fit
      height="100%"
      highlight-current-row
    >
      <el-table-column
        prop="date"
        label="日期"
        width="180"
      />
      <el-table-column
        prop="name"
        label="姓名"
        width="180"
      />
      <el-table-column
        prop="address"
        label="地址"
      />
    </el-table>
    <div class="app-footer">
      <el-pagination
        background
        layout="total, sizes, prev, pager, next"
        :total="table.total"
        :page-sizes="[5, 10, 15, 20, 50, 100]"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      table: {
        total: 100,
        list: [{
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }]
      }

    }
  }
}
</script>

<style lang="scss" scoped>
.app-container {
  height: 100%;
  overflow-y: hidden;
  display: flex;
  flex-direction: column;
}

.datatable-wrapper {
  height: 100%;
  display: flex;
  flex-direction: column;
}

.app-body {
  height: calc(100% - 40px);
}

.app-header {
  margin-bottom: 20px;
}

.app-footer {
  margin-top: 20px;
}
</style>
