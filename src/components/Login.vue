<template>
<div class="login">
  <el-form status-icon :rules="rules" ref="form" :model="form" label-width="80px">
    <img src="@/assets/head.jpg" alt="">
    <el-form-item label="用户名" prop="username">
      <el-input v-model="form.username" placeholder="请输入用户名"></el-input>
    </el-form-item>
    <el-form-item label="密码" prop="password">
      <el-input v-model="form.password" type="password" placeholder="请输入密码"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="login">登录</el-button>
      <el-button @click="reset">重置</el-button>
    </el-form-item>
  </el-form>
</div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      form: {
        username: '',
        password: ''
      },
      rules: {
        username: [
          { required: true, message: '用户名不能为空', trigger: 'blur' },
          { min: 3, max: 6, message: '长度在 3 到 6 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '密码不能为空', trigger: 'blur' },
          { min: 6, max: 12, message: '长度在 6 到 12 个字符', trigger: 'blur' }
        ]
      }
    }
  },

  methods: {
    login() {
      this.$refs.form.validate(valid => {
        if (valid) {
          axios({
            method: 'post',
            url: 'http://localhost:8888/api/private/v1/login',
            data: this.form
          }).then(res => {
            // console.log(res.data)
            if (res.data.meta.status === 200) {
              this.$message.success('登录成功')
              localStorage.setItem('token', res.data.data.token)

              this.$router.push('/home')
            } else {
              this.$message.error(res.data.meta.msg)
            }
          })
        } else {
          return false
        }
      })
    },
    reset() {
      this.$refs.form.resetFields()
    }
  }
}
</script>

<style lang="less">
.login {
  height: 100%;
  background-color: #2d434c;
  overflow: hidden;
  .el-form {
    width: 400px;
    background-color: #fff;
    margin: 200px auto;
    padding: 75px 40px 15px;
    position: relative;
    img {
      width: 100px;
      height: 100px;
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      top: -70px;
      border-radius: 50%;
      border: 10px solid #fff;
    }
    .el-button:nth-child(2) {
      margin-left: 80px;
    }
  }
}
</style>
