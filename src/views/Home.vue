<template>
  <el-container class="home_page">
    <el-header>
      <el-row>
        <el-col :span="20">
          <el-menu
          mode="horizontal"
          :default-active="curIndex"
          @select="select"
          background-color="#000"
          text-color="#fff"
          active-text-color="#ffd04b">
          <el-menu-item index="1">
            <span slot="title">欢迎界面</span>
          </el-menu-item>
          <el-menu-item index="3">
            <span slot="title">商品列表</span>
          </el-menu-item>
          <el-menu-item index="5">
            <span slot="title">购物车</span>
          </el-menu-item>
          <el-menu-item index="2" v-if="isAdmin">
            <span slot="title">用户管理</span>
          </el-menu-item>
          <el-menu-item index="4" v-if="isAdmin">
            <span slot="title">数据分析</span>
          </el-menu-item>
        </el-menu>
        </el-col>
        <el-col :span="2">
          <h6>当前用户：{{ user }}</h6>
        </el-col>
        <el-col :span="1">
          <el-button type="info" plain @click="logout">退出</el-button>
        </el-col>
      </el-row>
    </el-header>
    <el-container>
      <el-container>
        <el-main>
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </el-container>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: 'Home',
  data() {
    return {
    }
  },
  methods: {
    logout() {
      // sessionStorage.removeItem('user');
      this.$router.push('/')
    },
    select(index) {
      index == 1 ? this.$router.push('/home/welcome') : 
      index == 2 ? this.$router.push('/home/user') :
      index == 3 ? this.$router.push('/home/goods') :
      index == 4 ? this.$router.push('/home/analysis') :
      index == 5 ? this.$router.push('/home/shopping') : ''
    }
  },
  computed: {
    ...mapState({
      user: state => state.user,
      isAdmin: state => state.isAdmin
    }),
    curIndex() {
      let index = ''
      const name = this.$route.name
      if(name === 'Analysis') {
        index = '4'
      } else if(name === 'Goods') {
        index = '3'
      } else if(name === 'Welcome') {
        index = '1'
      } else if(name === 'User') {
        index = '2'
      } else if(name === 'Shopping') {
        index = '5'
      }
      return index 
    }
  }
}
</script>

<style lang="scss" scoped>
.home_page {
  width: 100%;
  height: 100%;
  .el-header {
    color: #fff;
    background-color: #000;
    border-bottom: 1px solid rgb(34, 33, 33);
    h4 {
      height: 100%;
      line-height: 100%;
    }
    .el-button {
      border-radius: 0;
      margin-top: 10px;
    }
  }
  .el-aside {
    background-color: #000;
    .el-menu {
      .el-menu-item {
        width: 249px !important;
        background-color: #000 !important;
      }
    }
  }
}
</style>
