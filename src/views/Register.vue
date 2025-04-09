<template>
  <div class="register-container">
    <div class="register-box">
      <h1 class="title">创建账号</h1>
      <div class="form-group">
        <input 
          type="text" 
          v-model="nickname" 
          class="cute-input" 
          placeholder="请输入昵称"
          autocomplete="off"
        >
      </div>
      <div class="form-group">
        <input 
          type="password" 
          v-model="password" 
          class="cute-input" 
          placeholder="请输入密码"
          autocomplete="new-password"
        >
      </div>
      <div class="form-group">
        <input 
          type="password" 
          v-model="confirmPassword" 
          class="cute-input" 
          placeholder="请确认密码"
          autocomplete="new-password"
        >
      </div>
      <button class="cute-button" @click="handleRegister">注册</button>
      <p class="login-link">
        已有账号？
        <router-link to="/login">立即登录</router-link>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Register',
  data() {
    return {
      nickname: '',
      password: '',
      confirmPassword: ''
    }
  },
  methods: {
    handleRegister() {
      if (!this.nickname || !this.password || !this.confirmPassword) {
        alert('请填写完整信息')
        return
      }
      if (this.password !== this.confirmPassword) {
        alert('两次输入的密码不一致')
        return
      }
      // 这里添加注册逻辑
      localStorage.setItem('user', JSON.stringify({
        nickname: this.nickname
      }))
      this.$router.push('/home')
    }
  }
}
</script>

<style scoped>
.register-container {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  background-color: var(--background-color);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.register-box {
  width: 100%;
  max-width: 320px;
  padding: 30px 20px;
  background: white;
  border-radius: 20px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  margin: 20px;
}

.title {
  text-align: center;
  color: var(--primary-color);
  margin-bottom: 30px;
  font-size: 1.8rem;
  font-weight: 600;
}

.form-group {
  margin-bottom: 20px;
}

.login-link {
  text-align: center;
  margin-top: 20px;
  font-size: 0.9rem;
  color: #666;
}

.login-link a {
  color: var(--primary-color);
  text-decoration: none;
  font-weight: 500;
}

.login-link a:active {
  opacity: 0.8;
}

@media screen and (max-height: 600px) {
  .register-box {
    padding: 20px;
    margin: 10px;
  }
  
  .title {
    margin-bottom: 20px;
    font-size: 1.5rem;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
}
</style> 