<template>
  <div class="main">
    <h1>Log-In</h1>
    <div class="loginBox">
      <input class="email" placeholder="Email" v-model="email" type="email"></input>
      <input class="password" placeholder="Password" v-model="password" type="password" v-on:keypress.enter="login"></input>
      <h3 class="logged">Stay logged In?<input type="checkbox" v-model="stayLogged"></input></h3>
      <button class="login" v-on:click="login">Submit</button>
      <h2 class="registerlink" v-on:click="$router.push('/Register')">Create a New Account Here</h2>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'Login',
    props: ['logged'],
    data () {
      return {
        email: '',
        password: '',
        stayLogged: false,
        user: {
          token: '',
          id: '',
          role: ''
        }
      }
    },
    created () {
      if (this.logged === true) {
        this.$router.push('/account')
      }
    },
    methods: {
      login () {
        let vue = this
        axios.post('http://54.219.138.159:81/users/login', {
          email: vue.email.toLowerCase(),
          password: vue.password
        })
          .then(response => {
            if (response.status !== 401) {
              vue.user.token = response.data.token
              vue.user.id = response.data.userId
              vue.user.role = response.data.role
              if (vue.stayLogged === true) {
                localStorage.setItem('token', response.data.token)
                localStorage.setItem('userId', response.data.userId)
                localStorage.setItem('role', response.data.role)
              }
              else {
                localStorage.removeItem('token')
                localStorage.removeItem('userId')
                localStorage.removeItem('role')
              }
              vue.$emit('login', vue.user)
            }
          })
          .catch(response => {
            console.log(response)
            this.wrong = true
          })
      }
    }
  }
</script>

<style scoped lang="less">
  @nvmgrey: #dae5ed;
  @nvmblue: #005389;
  @nvmred: #b20938;
  @nvmlightred: #e21b3c;
  .main {
    height: 500px;
    width: 100%;
    margin-top: 120px;
    text-align:center;
  }

  h1 {
    color: @nvmlightred;
  }

  .registerlink {
    font-size: 1.3em;
    color: #005389;
  }

  .logged {
    font-size: 1.5em;
  }

  button {
    background: linear-gradient(#005DA6, #014271);
    color: #fff;
    border: none;
    font-size: 1.7em;
  }

  input {
    border: 1px solid @nvmblue;
    margin-top: 5px;
    height: 30px;
  }

  @media (min-width: 700px) {
  }
</style>
