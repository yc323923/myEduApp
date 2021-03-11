<template>
  <div class="login">
    <div>
    <h2 class="login-title">
      Boss管理系统
    </h2>
    <el-form class="login-form"  :rules="formRule"  label-position="top" ref="form" :model="form" label-width="80px">
      <el-form-item prop="phone" label="手机号">
      <el-input v-model="form.phone"></el-input>
      </el-form-item>
      <el-form-item prop="pwd" label="密码">
      <el-input type="password" v-model="form.pwd"></el-input>
      </el-form-item>
    <el-form-item>
    <el-button class="login-btn" type="primary" @click="onSubmit('form')">登录</el-button>
    <!-- <el-button>取消</el-button> -->
    </el-form-item>
    </el-form>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
const validatorPhone = (rule: any, value: any, callback: Function) => {
  if (value === '') {
    callback(new Error('手机号不能为空'))
  } else if (!/^1\d{10}$/.test(value)) {
    callback(new Error('手机号格式错误'))
  }
}
const validatorPwd = (rule: any, value: string, callback: Function) => {
  if (value === '') {
    callback(new Error('密码不能为空'))
  } else if (value.trim().length < 3) {
    callback(new Error('密码至少3位'))
  }
}
export default Vue.extend({
  name: 'LoginIndex',
  data () {
    return {
      formRule: {
        pwd: [
          { required: true, validator: validatorPwd, trigger: 'blur' }
        ],
        phone: [
          { required: true, trigger: 'blur', validator: validatorPhone }
        ]
      },
      form: {
        phone: '',
        pwd: ''
      }
    }
  },
  methods: {
    onSubmit (form: string) {
      (this.$refs[form] as any).validate((isValid: boolean, obj: Object) => {
        if (isValid) {
          console.log('submit!')
        } else {
          alert('手机号或密码不对')
          return false
        }
      })
    }
  }
})
</script>

<style lang="scss" scoped>
.login {
  height:100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.login-form{
  background-color: #fff;
  width: 350px;
  padding: 20px;
  border-radius: 6px;
}
.login-btn{
  width: 100%;
}
.login-title{
  text-align: center;
}
</style>
