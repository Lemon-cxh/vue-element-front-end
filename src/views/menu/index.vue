<template>
  <el-card style="margin: 0px">
    <el-card >
      <el-container>

        <template>
          <el-aside width="25%" style="margin-top: 20px">
            <el-card shadow="hover">
              <el-tree
                :props="props"
                :load="loadNode"
                lazy
                @node-click="nodeClick">
              </el-tree>
            </el-card>
            <div style="margin-top: 15px" align="center">
              <el-button size="mini" type="primary">新增模块</el-button>
              <el-button size="mini" type="danger">删除模块</el-button>
            </div>
          </el-aside>
        </template>
        <template>
          <el-main>
            <el-card>
              <el-form :model="permissionForm" :rules="permissionForm" ref="permissionForm" label-width="100px" size="small" class="permissionForm">
                <el-row>
                  <el-col :span="12">
                    <el-form-item label="权限标识" prop="identify">
                      <el-input v-model="permissionForm.identify"></el-input>
                    </el-form-item>
                  </el-col>
                  <el-col :span="12">
                    <el-form-item label="权限名称" prop="permissionName">
                      <el-input v-model="permissionForm.permissionName"></el-input>
                    </el-form-item>
                  </el-col>
                </el-row>
                <el-row>
                  <el-col :span="12">
                    <el-form-item label="菜单图标" prop="menuIcon">
                      <el-input v-model="permissionForm.menuIcon"></el-input>
                    </el-form-item>
                  </el-col>
                  <el-col :span="12">
                    <el-form-item label="菜单父级" prop="parentIdentify">
                      <el-input v-model="permissionForm.parentIdentify"></el-input>
                    </el-form-item>
                  </el-col>
                </el-row>
                <el-row>
                  <el-col :span="12">
                    <el-form-item label="菜单路径" prop="menuPath">
                      <el-input v-model="permissionForm.menuPath"></el-input>
                    </el-form-item>
                  </el-col>
                  <el-col :span="12">
                    <el-form-item label="菜单排序" prop="menuOrder">
                      <el-input v-model="permissionForm.menuOrder"></el-input>
                    </el-form-item>
                  </el-col>
                </el-row>
                <el-row>
                  <el-form-item label="菜单备注信息" prop="menuNote">
                    <el-input type="textarea"
                              :rows="2"
                              placeholder="菜单模块描述信息"
                              v-model="permissionForm.menuNote">
                    </el-input>
                  </el-form-item>
                </el-row>
                <el-form-item style="margin-left: 25%">
                  <el-button type="primary" size="mini">提交修改</el-button>
                  <!--<el-button >重置</el-button>-->
                  <!--&lt;!&ndash;<el-button type="danger">删除</el-button>&ndash;&gt;-->
                </el-form-item>
              </el-form>

            </el-card>
            <el-card style="margin-top: 15px">
              <div style="margin-bottom: 15px">
                <el-button size="mini" type="primary">新增权限</el-button>
              </div>
              <el-table :data="tableData" size="small"  style="width: 100%; border-top: 1px solid #eaeefb">

                <el-table-column label="序号" width="180" align="center" >
                  <template slot-scope="scope" >
                    <span style="margin-left: 10px">{{ scope.row.id }}</span>
                  </template>
                </el-table-column>

                <el-table-column label="权限标识" width="180" align="center">
                  <template slot-scope="scope" >
                    <el-popover trigger="hover" placement="top">
                      <p>权限标识: {{ scope.row.identification }}</p>
                      <p>描述信息: {{ scope.row.note }}</p>
                      <div slot="reference" class="name-wrapper">
                        <el-tag size="medium">{{ scope.row.identification }}</el-tag>
                      </div>
                    </el-popover>
                  </template>

                </el-table-column>

                <el-table-column label="权限状态" width="180" align="center">
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
                      type="danger"
                      @click="handleDelete(scope.$index, scope.row)">删除</el-button>
                  </template>
                </el-table-column>
              </el-table>
            </el-card>
          </el-main>
        </template>
      </el-container>
    </el-card>
  </el-card>


</template>

<script>
  /* eslint-disable indent */

  export default {
    data() {
      return {
        props: {
          label: 'name',
          children: 'zones'
        },
        count: 1,
        permissionForm: {
          identify: '',
          permissionName: '',
          menuIcon: '',
          parentIdentify: '',
          menuPath: '',
          menuOrder: '',
          menuNote: ''

        },
        tableData: [{
          id: 1,
          identification: 'M',
          status: 0,
          note: '菜单可见权限'
        }, {
          id: 2,
          identification: 'R',
          status: 0,
          note: '查询权限'
        }, {
          id: 3,
          identification: 'C',
          status: 100,
          note: '新增权限'
        }, {
          id: 4,
          identification: 'U',
          status: 100,
          note: '更新权限'
        }, {
            id: 4,
          identification: 'D',
          status: 100,
            note: '删除权限'
        }],
        treeData: [{
          id: 'funds',
          name: '资金管理',
          parentId: '-1'
        }, {
            id: 'getmoney',
            name: '提现记录',
            parentId: 'funds'
        }, {
          id: 'root',
          name: '基础管理',
          parentId: '-1'
        }, {
          id: 'info',
          name: '提现详情',
          parentId: 'getmoney'
        }]
      }
  },
    methods: {
      nodeClick(data, node, itself) {
        console.info(data)
        console.info(node)
        console.info(itself)
      },
      loadNode: function(node, resolve) {
        if (node.level === 0) {
          const data = []
          for (let i = 0; i < this.treeData.length; i++) {
            if (this.treeData[i].parentId === '-1') {
              const d = {}
              d.name = this.treeData[i].name
              d.id = this.treeData[i].id
              data.push(d)
            }
          }
          return resolve(data)
        }
        if (node.level > 0) {
          const data = []
          for (let i = 0; i < this.treeData.length; i++) {
            if (this.treeData[i].parentId === node.data.id) {
              const d = {}
              d.name = this.treeData[i].name
              d.id = this.treeData[i].id
              data.push(d)
            }
          }
          resolve(data)
        }
      },
      handleDelete: function(index, row) {
        console.log(index, row)
    }
    }
  }
</script>
