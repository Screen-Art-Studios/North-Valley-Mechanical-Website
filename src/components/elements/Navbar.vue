<template>
  <div class="main">
    <div class="navbar">
      <div v-bind:class="nvLogic" v-on:click="navToggle"></div>
      <div v-bind:class="navpaneLogic">
        <button class="Home" v-on:click="navToggle(); $router.push('/')" v-if="!app">Home</button>
        <button class="Services" v-on:click="navToggle(); $router.push('/Services')" v-if="!app">Services</button>
        <button class="Reviews" v-on:click="navToggle(); $router.push('/Reviews')">Reviews</button>
        <button class="Contact" v-on:click="navToggle(); $router.push('/Contact')">Contact</button>
        <button class="Services" v-on:click="navToggle(); $router.push('/Specials')" v-if="app && (user.role !== 'employee')">Specials</button>
        <button class="Login" v-on:click="navToggle(); $router.push('/Messaging')" v-if="logged && app && (user.role === 'employee')">Messaging</button>
        <button class="Login" v-on:click="navToggle(); $router.push('/Login')" v-if="!logged">Login</button>
        <button class="Login" v-on:click="navToggle(); $router.push('/Account')" v-if="logged">Account</button>
        <button class="Login" v-on:click="navToggle(); $emit('logout')" v-if="logged && app">Logout</button>
    </div>
  </div>
</div>
</template>

<script>
  export default {
    name: 'navbar',
    props: ['logged', 'user', 'app'],
    data () {
      return {
        toggled: false,
        isToggled: false,
        first: true
      }
    },
    methods: {
      navToggle: function () {
        // Nav button functionality
        if (window.innerWidth < 700) {
          if (this.toggled === false) {
            this.toggled = true
            this.isToggled = true
            this.first = false
          }
          else if (this.toggled === true) {
            this.toggled = false
            this.isToggled = false
          }
        }
        else {
          this.$router.push('/')
        }
      }
    },
    computed: {
      nvLogic: function () {
        return {
          nv: true,
          navButtonAnimation: this.isToggled,
          navButtonAnimationExit: !this.isToggled && !this.first
        }
      },
      navpaneLogic: function () {
        return {
          navpane: this.first,
          navpaneAnimation: this.isToggled,
          navpaneAnimationExit: !this.isToggled && !this.first
        }
      }
    }
  }
</script>

<style scoped lang="less">
@nvmgrey: #dae5ed;
@nvmblue: #005389;
@nvmred: #b20938;

  .navpane {
    display: none;
    overflow: hidden;
  }

  .main {
    width: 100%;
  }

  .nv {
    margin-top: 20px;
    width: 80px;
    height: 80px;
    overflow: hidden;
    margin-top: 10px;
    margin-right: 10px;
    grid-column: 4;
    z-index: 8;
    background-repeat: no-repeat;
    background-image: url("../../assets/navbuttonAnimationWhite.svg");
  }

  .navbar {
    width: 100%;
    height: 100px;
    background: linear-gradient(#005DA6, #014271);
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 11;
    text-align: center;
    line-height: 70px;
    font-weight: lighter;
    display: grid;
    grid-template-columns: repeat(2, 1fr) 220px repeat(2,1fr);
    grid-template-rows: 100px;
  }

  .navpaneAnimation {
    animation: navpaneAnimation .3s steps(9);
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
    grid-column-start: 2;
    grid-column-end: 5;
    z-index: 10;
    width: 100%;
    height: 400px;
    margin-top: 1px;
    background: linear-gradient(#e21b3c, #b20938);
    color: #fff;
    outline: solid 1px ;
    outline-color: #fff;
    box-shadow: 0px 1px 1px 2px #fff;
  }

  .navpaneAnimationExit {
    animation: navpaneAnimationReverse .3s steps(9);
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
    display: none;
  }

  .navpaneAnimationExit button {
    display: none;
  }

  .Home {
    box-shadow: none;
    background-color: transparent;
    border: none;
    color: #fff;
    font-size: 2.5em;
    width: 100%;
    font-weight: normal;
  }

  .Reviews {
    background-color: transparent;
    width: 100%;
    background-color: transparent;
    border: none;
    color: #fff;
    font-size: 2.5em;
    font-weight: normal;
  }

  .Contact {
    background-color: transparent;
    width: 100%;
    background-color: transparent;
    border: none;
    color: #fff;
    font-size: 2.5em;
    font-weight: normal;
  }

  .Services {
    background-color: transparent;
    width: 100%;
    background-color: transparent;
    border: none;
    color: #fff;
    font-size: 2.5em;
    font-weight: normal;
  }

  .Login {
    background-color: transparent;
    width: 100%;
    background-color: transparent;
    border: none;
    color: #fff;
    font-size: 2.5em;
    font-weight: normal;
  }

  @keyframes navpaneAnimation {
    0% { opacity: 0; }
    100% { opacity: 1; }
  }

  @keyframes navpaneAnimationReverse {
    0% { opacity: 1; }
    100% { opacity: 0; display: none;}
  }

  @keyframes navButtonAnimation {
    100% {background-position: -1440px;}
  }

  @keyframes navButtonAnimationReverse {
    0% {background-position: -1440px;}
    100% {background-position: 0px;}
  }

  .navButtonAnimation {
    animation: navButtonAnimation .35s steps(18);
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
  }

  .navButtonAnimationExit {
    animation: navButtonAnimationReverse .35s steps(18);
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
  }

  .hidden {
    display: none;
  }

  @media (min-width: 700px) {
    .navpane {
      width: 100%;
      height: 120px;
      z-index: 3;
      text-align: center;
      line-height: 70px;
      font-weight: lighter;
      display: grid;
      grid-template-columns: repeat(2, 1fr) 220px repeat(2,1fr);
      grid-template-rows: 100px;
    }

    .nv {
      display: none;
    }
  }
</style>
