<template>
  <div class="yb-main-header">
    <h3 class="yb-title">{{$store.state.globalSettings.appName}}管理后台</h3>
    <div class="yb-right">
      当前用户:{{$store.state.adminName}}
      <el-button size="mini" @click="quit">退出</el-button>
    </div>
  </div>
</template>

<script>
  export default {
    methods: {
      quit(){
        //清除当前用户的登录信息
        this.$store.commit('setAdminName','')
        //跳转回登录页
        this.$router.push('/login')
      }
    },
  }
</script>