<template>
  <div class="header">
      <el-breadcrumb separator="/">
  <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
  <el-breadcrumb-item>活动管理</el-breadcrumb-item>
  <el-breadcrumb-item>活动列表</el-breadcrumb-item>
  <el-breadcrumb-item>活动详情</el-breadcrumb-item>
</el-breadcrumb>

<el-dropdown>
  <span class="el-dropdown-link">
      <el-avatar :size="30" :src="userInfo.portrait"></el-avatar>
      <span class="space-text"></span>
  </span>
  <el-dropdown-menu slot="dropdown">
    <el-dropdown-item>{{userInfo.userName}}</el-dropdown-item>
    <el-dropdown-item @click.native="handleLogout" divided>退出</el-dropdown-item>
  </el-dropdown-menu>
</el-dropdown>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { getUserInfo } from '@/services/user'
export default Vue.extend({
  name: 'AppHeader',
  data () {
    return {
      userInfo: {} // 当前登录用户信息
    }
  },
  created () {
    this.loadUserInfo()
    this.loadUserInfo()
    this.loadUserInfo()
  },
  methods: {
    async loadUserInfo () {
      const { data } = await getUserInfo()
      this.userInfo = data.content
    },

    handleLogout () {
      this.$confirm('确认退出吗？', '退出提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => { // 确认执行这里
        // 清除登录状态
        this.$store.commit('setUser', null)

        // 跳转到登录页面
        this.$router.push({
          name: 'login'
        })

        this.$message({
          type: 'success',
          message: '退出成功!'
        })
      }).catch(() => { // 取消执行这里
        this.$message({
          type: 'info',
          message: '已取消退出'
        })
      })
    }
  }
})
</script>
<style lang="scss" scoped >
.header {
    display: flex;
    align-items: center;
    height: 100%;
    justify-content: space-between;
}
.space-text {
    display: inline-block;
    width: 30px;
}
</style>
