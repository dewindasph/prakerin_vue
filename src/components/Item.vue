<template>
  <el-row class="login-style">
    <h1>Welcome</h1>
    <el-input placeholder="username" v-model="username"></el-input>
    <el-input type="password" placeholder="password" v-model="password"></el-input>
    <el-input type="password" placeholder="retype password" v-if = "type === 'register'" v-model="re_password"></el-input>
    <el-button type="primary" v-if = "type === 'register'" @click="signup()">Submit</el-button>
    <el-button type="primary" v-else @click="login()">submit</el-button>
  <br>
    <el-button type="primary" @click="getData()">get data</el-button>

    <router-link to="/login" v-show = "type === 'register'" tag="p">Already Have an Account? Sign in</router-link>
    <router-link to="/register" v-show = "type === 'login'" tag="p">Don't Have an Account? Sign up</router-link>
  </el-row>
</template>

<script>
export default {
  data () {
    return {
      username: '',
      password: '',
      re_password: '',
      sayhub_token: ''
    }
  },
  props: {
    type: {
      type: String
    }
  },
  methods: {
    // 注册
    signup () {
    },
    // 登陆
    login () {
      if (this.username === '') {
        this.$message.warning('Username tidak boleh kosong~~')
      } else if (this.password === '') {
        this.$message.warning('Password tidak boleh kosong~~')
      } else {
        this.$store.dispatch('toLogin', {
          loginUser: this.username,
          loginPassword: this.password
        }).then(() => {
          this.$store.dispatch('getUser')
          let redirectUrl = decodeURIComponent(this.$route.query.redirect || '/')
          console.log(redirectUrl)
          // 跳转到指定的路由
          this.$router.push({
            path: redirectUrl
          })
        }).catch((error) => {
          console.log(error.response.data.message)
        })
      }
    },

    getData(){
      fetch( 'https://www.pps-stie-nobel.org/api/harlem/detail/?id=1', {
      method: 'GET',
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded',
        'x-api-key'     : 'A7980EB02ADE9DD9FD90DDAB0AEF1676',
        'x-token'       : 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJkYXRhIjp7ImlkIjoiMzE5OCJ9LCJpYXQiOjE2NzM0Nzg3NzEsImV4cCI6MTY3MzU2NTE3MX0.3NYjQjfImaXwW6c0OZPajG6_NNiCx-iybATcBaEpKWU'
    },

    body: null,
  } ).then(res => {
              return res.json();
          })
          .then(tickets => {
                alert(tickets.data.harlem.firstName);
          }) ;
      },

    doLogin(){
    var data = new URLSearchParams();
    data.append('username', 'vue');
    data.append('password', '12345678');

    const requestOptions = {
    method: "POST",
    headers: {
       "Content-Type": "application/x-www-form-urlencoded",
      "x-api-key": "A7980EB02ADE9DD9FD90DDAB0AEF1676"
    },
    body: data
    };
    fetch("https://pps-stie-nobel.org/api/user/login", requestOptions)
    .then(response => response.json())
    .then(data => (this.postId = data.id));
  }
   }
    }

</script>

<style scoped>
.login-style {
  border: 1px solid #fff;
  text-align: center;
  padding: 20px;
  line-height: 50px;
  background: #fff;
  width: 300px;
  box-shadow: 0 1px 3px 0 rgba(210, 130, 226, 0.5);
}
p {
  font-size: 12px;
  cursor: pointer;
}
</style>
