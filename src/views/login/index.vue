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
      <el-form-item prop="password" label="密码">
      <el-input type="password" v-model="form.password"></el-input>
      </el-form-item>
    <el-form-item>
    <el-button :disabled='disabledBtn' class="login-btn" type="primary" @click="onSubmit()">登录</el-button>
    <!-- <el-button>取消</el-button> -->
    </el-form-item>
    </el-form>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { login } from '@/services/user'
import { Form } from 'element-ui'
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
interface LoginRes {
  state: number;
  content: string;
  message: string;
  success: boolean;
}
export default Vue.extend({
  name: 'LoginIndex',
  data () {
    return {
      disabledBtn: false,
      formRule: {
        password: [
          { required: true, trigger: 'blur' }
        ],
        phone: [
          { required: true, trigger: 'blur' }
        ]
      },
      form: {
        phone: '18201288771',
        password: '111111'
      }
    }
  },
  methods: {
    async onSubmit () {
      const isValid = await (this.$refs.form as Form).validate()
      if (!isValid) return
      this.disabledBtn = true
      login(this.form).then((ret) => {
        const data: LoginRes = ret.data
        if (data.state === 1) {
          this.$store.commit('setUser', data.content)
          this.$message.success(data.message)
          this.disabledBtn = false
          this.$router.push(this.$route.query.redirect as string || '/')
        } else {
          this.$message.error(data.message)
          this.disabledBtn = false
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
