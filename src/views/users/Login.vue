<template>
  <div>
    <div class="loading-wrapper" v-show="showLoading">
      <Loading></Loading>
    </div>
    <div class="login-wrapper" v-show="!showLoading">
      <img :src="imgUrl" alt="" width="100%" height="100%">
      <div class="login">
        <p class="title">Vue-Element-Demo</p>
        <el-form
          :model="ruleForm"
          status-icon
          :rules="rules"
          ref="ruleForm"
          label-width="0"
          class="demo-ruleForm"
        >
          <el-form-item prop="name">
            <el-input v-model="ruleForm.name" auto-complete="off" placeholder="请输入用户名"></el-input>
          </el-form-item>
          <el-form-item prop="pass">
            <el-input type="password" v-model="ruleForm.pass" auto-complete="off" placeholder="输入密码"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="login('ruleForm')" style="width:100%;">登录</el-button>
            <p class="register" @click="gotoRegist">没有账户？立即注册</p>
          </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
</template>

<script>
import { mapMutations } from 'vuex'
// import axios from 'axios'
import Loading from '@/components/loading/Loading.vue'
export default {
  name: 'Login',
  components: {
    Loading
  },
  data() {
    let checkName = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入用户名'))
      } else {
        callback()
      }
    }
    let validatePass = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"))
      } else {
        callback()
      }
    }
    return {
      showLoading: true,
      imgUrl: require('../../assets/images/bg-img-1.jpg'),
      ruleForm: {
        name: '',
        pass: ''
      },
      rules: {
        name: [{ validator: checkName, trigger: 'change' }],
        pass: [{ validator: validatePass, trigger: 'change' }],
      }
    }
  },
  mounted () {
    let bgImg = new Image()
    bgImg.src = this.imgUrl
    bgImg.onerror = () => {
      console.log('img onerror')
    }
    bgImg.onload = () => { // 图片加载成功后 去除loading
      this.showLoading = false
    }
  },
  methods: {
    ...mapMutations({
      bindLogin: 'BIND_LOGIN',
      saveUser: 'SAVE_USER'
    }),
    login(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          this.bindLogin(this.ruleForm.name)
          this.saveUser(this.ruleForm.name)
          this.$notify({
            title: '成功',
            message: '恭喜，登录成功。',
            duration: 1000,
            type: 'success'
          })
          setTimeout(() => {
            this.$router.push({
              path: '/'
            })
          }, 500)
        }
      })
    },
    gotoRegist () {
      this.$router.push({
        path: '/demo'
      })
    }
  }
}
</script>

