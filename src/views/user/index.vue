<template>
  <el-card style="margin: 5px">
    <el-card>
      <div style="margin-bottom: 15px">
        <el-button size="mini" type="primary">新增用户</el-button>
        <el-input size="mini" placeholder="请输入搜索内容" v-model="input" class="input-with-select" style="float: right">
          <el-select v-model="select" slot="prepend" placeholder="请选择搜索范围">
            <el-option label="登陆名" value="1"></el-option>
            <el-option label="账号状态" value="2"></el-option>
            <el-option label="用户电话" value="3"></el-option>
          </el-select>
          <el-button slot="append" icon="el-icon-search" ></el-button>
        </el-input>
      </div>
      <el-table :data="tableData" size="small"  height="450" style="width: 100%; border-top: 1px solid #eaeefb">

        <el-table-column label="序号" width="180" align="center" >
          <template slot-scope="scope" >
            <span style="margin-left: 10px">{{ scope.row.id }}</span>
          </template>
        </el-table-column>

        <el-table-column label="登陆名" width="180" align="center">
          <template slot-scope="scope" >
            <el-popover trigger="hover" placement="top">
              <p>用户名: {{ scope.row.identification }}</p>
              <p>描述信息: {{ scope.row.note }}</p>
              <div slot="reference" class="name-wrapper">
                <el-tag size="medium">{{ scope.row.identification }}</el-tag>
              </div>
            </el-popover>
          </template>

        </el-table-column>

        <el-table-column label="账号状态" width="180" align="center">
          <template slot-scope="scope">
            <el-switch v-model="scope.row.status" active-color="#13ce66"
                       inactive-color="#ff4949"
                       active-value="100"
                       inactive-value="0"
                       style="margin: 1px">
            </el-switch>
          </template>
        </el-table-column>
        <el-table-column label="操作" align="center">
          <template slot-scope="scope">
            <el-button
              size="mini"
              type="warning"
              @click="handleDelete(scope.$index, scope.row)">修改</el-button>
            <el-button
              size="mini"
              type="danger"
              @click="handleDelete(scope.$index, scope.row)">删除</el-button>
          </template>
        </el-table-column>
      </el-table>
      <div class="block" align="center" style="margin-top: 15px">
        <el-pagination
          background
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage"
          :page-sizes="[10, 15, 20, 25]"
          :page-size="10"
          layout="total, sizes, prev, pager, next, jumper"
          :total="10000">
        </el-pagination>
      </div>
    </el-card>

  </el-card>
</template>

<script>
  export default {
    data() {
      return {
        tableData: [{
          id: 1,
          identification: 'admin',
          status: 0,
          note: '系统超级管理员'
        }, {
          id: 2,
          identification: 'Sissy',
          status: 0,
          note: '系统管理员'
        }, {
          id: 3,
          identification: 'Arnold',
          status: 100,
          note: '普通用户'
        }, {
          id: 4,
          identification: 'Johny',
          status: 100,
          note: '普通用户'
        }, {
          id: 4,
          identification: 'jobs',
          status: 100,
          note: '普通用户'
        }],
        currentPage: 1,
        input: '',
        select: ''
      }
    },
    methods: {
      handleDelete: function(index, row) {
        console.log(index, row)
      },
      handleSizeChange(val) {
        console.log(`每页 ${val} 条`)
      },
      handleCurrentChange(val) {
        console.log(`当前页: ${val}`)
      }
    }
  }
</script>
<style>
  /*搜索框 添加按钮列样式 begin */
  .el-select .el-input {
    width: 130px;
  }
  .input-with-select {
    background-color: #fff;
  }
  .el-input-group {
    width:30%;
  }
  .el-input--suffix {
    padding-right: 10px;
  }
  .el-input--suffix .el-input__inner {
    padding-right: 10px;
  }
  .el-select .el-input.is-focus .el-input__inner {
     border-color: #f5f7fa;
  }
  /*搜索框 添加按钮列样式  end*/
</style>
