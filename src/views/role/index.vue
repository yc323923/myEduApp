<template>
  <div class="role">
    <RoleList/>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import RoleList from './components/list.vue'
export default Vue.extend({
  name: 'LoginIndex',
  components: {
    RoleList
  }
})
</script>

<style lang="scss" scoped></style>
