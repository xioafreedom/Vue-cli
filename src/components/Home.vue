<template>
    <el-container class="home">
      <el-header>
        <div class="logo"></div>
        <div class="title">
          <h1>电商后台管理系统</h1>
        </div>
        <div class="loginout">
          <span>欢迎光临</span>
          <a href="javascript:;" @click="loginout">退出</a>
        </div>
      </el-header>
      <el-container>
        <el-aside width="200px">Aside</el-aside>
        <el-main>Main</el-main>
      </el-container>
    </el-container>
</template>

<script>
export default {
  methods: {
    loginout() {
      localStorage.removeItem('token')
      this.$router.push('/login')
      this.$message.success('退出成功')
    }
  }
}
</script>

<style lang="less" scoped>
.home {
  height: 100%;
  .el-header {
    background-color: #b3c1cd;
    display: flex;
    .logo {
      width: 180px;
      background-image: url('~@/assets/logo.png');
      background-size: contain;
      background-repeat: no-repeat;
      background-position: center center;
    }
    .title {
      flex: 1;
      text-align: center;
      line-height: 60px;
      color: #fff;
      font-size: 26px;
    }
    .loginout {
      width: 180px;
      line-height: 60px;
      text-align: center;
      font-size: 18px;
      a {
        color: #545c64;
      }
    }
  }
  .el-aside {
    background-color: #545c64;
  }

  .el-main {
    background-color: #eaeef1;
  }
}
</style>
