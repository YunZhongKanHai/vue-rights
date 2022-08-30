<template>
  <div>
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>权限管理</el-breadcrumb-item>
      <el-breadcrumb-item>权限列表</el-breadcrumb-item>
    </el-breadcrumb>

    <el-card>
      <el-table :data="rightsList" border stripe>
        <el-table-column type="index" label="序号"></el-table-column>
        <el-table-column label="权限名称" prop="authName"></el-table-column>
        <el-table-column label="路径" prop="path"></el-table-column>
        <el-table-column label="权限等级" prop="level">
          <template slot-scope="scope">
            <el-tag v-if="scope.row.level === '0'">标签一</el-tag>
            <el-tag type="success" v-else-if="scope.row.level === '1'">标签二</el-tag>
            <el-tag type="warning" v-else>标签三</el-tag>
          </template>
        </el-table-column>
      </el-table>
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'vueRights',
  data () {
    return {
      rightsList: []
    }
  },
  methods: {
    async getRightsList () {
      const { data: res } = await this.$http.get('rights/list')
      // console.log(res)
      if (res.meta.status !== 200) return this.$message.error('获取用户列表数据失败！')
      this.rightsList = res.data
      // console.log(this.rightsList)
    }
  },
  created () {
    this.getRightsList()
  }
}
</script>

<style lang="less" scoped>
</style>
