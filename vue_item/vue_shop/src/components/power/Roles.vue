<template>
  <div>
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>权限管理</el-breadcrumb-item>
      <el-breadcrumb-item>角色列表</el-breadcrumb-item>
    </el-breadcrumb>

    <el-card>
      <el-row>
        <el-col>
          <el-button type="primary">添加角色</el-button>
        </el-col>
      </el-row>

      <el-table :data="roleList" border stripe>
        <el-table-column type="index" label="序号"></el-table-column>
        <el-table-column label="角色名称" prop="roleName"></el-table-column>
        <el-table-column label="角色描述" prop="roleDesc"></el-table-column>
        <el-table-column label="操作">
          <el-button size="mini" type="primary" icon="el-icon-edit">编辑</el-button>
          <el-button size="mini" type="danger" icon="el-icon-delete">删除</el-button>
          <el-button size="mini" type="warning" icon="el-icon-setting">分配权限</el-button>
        </el-table-column>
      </el-table>
    </el-card>

  </div>
</template>

<script>
export default {
  name: 'vueRoles',
  data () {
    // 这里存放数据
    return {
      roleList: []
    }
  },
  // 方法集合
  methods: {
    async getRolesList () {
      const { data: res } = await this.$http.get('roles')
      if (res.meta.status !== 200) return this.$message.error('获取角色列表数据失败！')
      this.roleList = res.data
      // console.log(this.roleList)
    }
  },
  // 生命周期 - 创建完成（可以访问当前this实例）
  created () {
    this.getRolesList()
  }
}
</script>

<style lang='less' scoped>
</style>
