<template>
  <div class="app-container">
    <el-dialog
      title="添加"
      :visible.sync="showAdd"
      width="800px"
      :close-on-click-modal="false"
    >
      <!-- 添加信息弹出框 -->
      <el-form ref="addForm" :model="addForm" label-width="80px">
        <el-form-item label="活动名称">
          <el-input v-model="addForm.name" />
        </el-form-item>
        <el-form-item label="活动区域">
          <el-select v-model="addForm.region" placeholder="请选择活动区域">
            <el-option label="区域一" value="shanghai" />
            <el-option label="区域二" value="beijing" />
          </el-select>
        </el-form-item>
        <el-form-item label="活动时间">
          <el-col :span="11">
            <el-date-picker v-model="addForm.date1" type="date" placeholder="选择日期" style="width: 100%;" />
          </el-col>
          <el-col class="line" :span="2">-</el-col>
          <el-col :span="11">
            <el-time-picker v-model="addForm.date2" placeholder="选择时间" style="width: 100%;" />
          </el-col>
        </el-form-item>
        <el-form-item label="即时配送">
          <el-switch v-model="addForm.delivery" />
        </el-form-item>
        <el-form-item label="活动性质">
          <el-checkbox-group v-model="addForm.type">
            <el-checkbox label="美食/餐厅线上活动" name="type" />
            <el-checkbox label="地推活动" name="type" />
            <el-checkbox label="线下主题活动" name="type" />
            <el-checkbox label="单纯品牌曝光" name="type" />
          </el-checkbox-group>
        </el-form-item>
        <el-form-item label="特殊资源">
          <el-radio-group v-model="addForm.resource">
            <el-radio label="线上品牌商赞助" />
            <el-radio label="线下场地免费" />
          </el-radio-group>
        </el-form-item>
        <el-form-item label="活动形式">
          <el-input v-model="addForm.desc" type="textarea" />
        </el-form-item>
      </el-form>
      <span
        slot="footer"
        class="dialog-footer"
      >
        <el-button
          type="success"
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
        @click="showAdd=true"
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
      // 添加部分
      showAdd: false,
      addForm: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: '',
        type: [],
        resource: '',
        desc: ''
      },
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
