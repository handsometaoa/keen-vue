<template>
  <div>
    <form
      class="form w-100 fv-plugins-bootstrap5 fv-plugins-framework"
      action="#"
    >
      <div class="fv-row mb-8 fv-plugins-icon-container">
        <el-input
          v-model="registerForm.username"
          style="width: 100%; height: 40px"
          placeholder="账号"
        />
      </div>

      <div class="fv-row mb-7 fv-plugins-icon-container">
        <el-input
          v-model="registerForm.password"
          type="password"
          :show-password="true"
          style="width: 100%; height: 40px"
          placeholder="密码"
        />
      </div>

      <div class="fv-row mb-7 fv-plugins-icon-container">
        <el-input
          v-model="registerForm.confirmPassword"
          type="password"
          :show-password="true"
          style="width: 100%; height: 40px"
          placeholder="确认密码"
        />
      </div>

      <div class="fv-row mb-7 fv-plugins-icon-container">
        <el-input
          v-model="registerForm.email"
          type="password"
          style="width: 100%; height: 40px"
          placeholder="邮箱"
        />
      </div>
    </form>
    <div class="d-flex flex-stack">
      <el-button
        style="width: 45%"
        type="primary"
        @click="register()"
      >注 册</el-button>
      <el-button
        style="width: 45%"
        type="danger"
        @click="clear()"
      >清 空</el-button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'UserRegister', // 这个LoginName最好和引入的vue的LoginName相同
  data() {
    return {
      registerForm: {
        username: '',
        password: '',
        confirmPassword: '',
        email: ''
      }
    }
  },
  methods: {
    clear() {
      this.registerForm.username = ''
      this.registerForm.password = ''
      this.registerForm.confirmPassword = ''
      this.registerForm.email = ''
    },
    register() {
      if (this.registerForm.password !== this.registerForm.confirmPassword) {
        console.log(this.registerForm.password)
        return
      }

      this.$store.dispatch('user/register', this.registerForm).then(() => {
        this.redirect = '/user'
        this.$router.push({
          path: this.redirect || '/',
          query: this.otherQuery
        })
      }).finally(() => {
        this.loadingBtn = false
      })
    }
  }
}
</script>
