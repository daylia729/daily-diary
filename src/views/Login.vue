<template>
  <div class="login-container">
    <div class="login-box">
      <h1 class="title">欢迎回来</h1>
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
          autocomplete="current-password"
        >
      </div>
      <button class="cute-button" @click="handleLogin">登录</button>
      <p class="register-link">
        还没有账号？
        <router-link to="/register">立即注册</router-link>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      nickname: '',
      password: ''
    }
  },
  methods: {
    handleLogin() {
      // 这里添加登录逻辑
      if (this.nickname && this.password) {
        // 模拟登录成功
        localStorage.setItem('user', JSON.stringify({
          nickname: this.nickname
        }))
        this.$router.push('/home')
      } else {
        alert('请填写完整信息')
      }
    }
  }
}
</script>

<style scoped>
.login-container {
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

.login-box {
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

.register-link {
  text-align: center;
  margin-top: 20px;
  font-size: 0.9rem;
  color: #666;
}

.register-link a {
  color: var(--primary-color);
  text-decoration: none;
  font-weight: 500;
}

.register-link a:active {
  opacity: 0.8;
}

@media screen and (max-height: 600px) {
  .login-box {
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