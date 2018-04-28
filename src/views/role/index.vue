<template>
  <el-card shadow="hover">
    <el-row class="role-card">
      <el-col :span="5" v-for="(o, index) in 8" :key="o" :offset="index > 0 ? 1 : 1" style="margin-bottom: 5px">
        <el-card :body-style="{ padding: '0px'}">
          <img src="src/assets/hamburger.png" class="image">
          <div style="padding: 14px;">
            <span>超级管理员</span>
            <div class="bottom clearfix" align="center">
              <el-tooltip placement="top">
                <div slot="content">多行信息<br/>第二行信息<br/>第二行信息<br/>第二行信息<br/>第二行信息<br/>第二行信息</div>
              <el-button type="warning" size="mini" icon="el-icon-star-off"></el-button>
              </el-tooltip>
              <el-tooltip placement="top">
                <div slot="content">编辑</div>
              <el-button type="primary" size="mini" icon="el-icon-edit"></el-button>
              </el-tooltip>
              <el-tooltip placement="top">
                <div slot="content">删除</div>
              <el-button type="danger" size="mini" icon="el-icon-delete"></el-button>
              </el-tooltip>
            </div>
          </div>
        </el-card>
      </el-col>
    </el-row>
  </el-card>
</template>

<script>
  export default {
    data() {
      return {
      }
    }
  }

</script>

<style scoped>

  .role-card{
    margin-top: 20px;
  }
  .bottom {
    margin-top: 13px;
    line-height: 12px;
  }

  .image {
    width: 100%;
    display: block;
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }

  .clearfix:after {
    clear: both
  }
</style>
