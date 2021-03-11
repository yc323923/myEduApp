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
      <el-avatar :size="30" src="https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png"></el-avatar>
      <span class="space-text"></span>
  </span>
  <el-dropdown-menu slot="dropdown">
    <el-dropdown-item>用户ID</el-dropdown-item>
    <el-dropdown-item divided>退出</el-dropdown-item>
  </el-dropdown-menu>
</el-dropdown>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'AppHeader'
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
