<template>
  <div id="nav">
    <div id="header">
      <h2 @click="goToLanding">KEMIN TONG</h2>
      <div></div>
      <h3 :style="home" @click="goToHome">
        <span v-if="this.$store.getters.languageGet">首页</span
        ><span v-else>HOME</span>
      </h3>
      <h3 :style="bio" @click="goToBio">
        <span v-if="this.$store.getters.languageGet">个人简介</span
        ><span v-else>BIO</span>
      </h3>
      <h3 :style="portfolio" @click="goToPortfolio">
        <span v-if="this.$store.getters.languageGet">作品集</span
        ><span v-else>PORTFOLIO</span>
      </h3>
      <h3 :style="contact" @click="goToContact">
        <span v-if="this.$store.getters.languageGet">与我联系</span
        ><span v-else>CONTACT</span>
      </h3>
      <button id="login-btn" @click="showInput">
        <span v-if="this.$store.getters.languageGet">管理员登录</span
        ><span v-else>admin login</span>
      </button>
    </div>
    <div v-if="show == false" id="login">
      <div></div>
      <div id="form">
        <h4>
          <span v-if="this.$store.getters.languageGet">用户名</span
          ><span v-else>Username</span>
        </h4>
        <input
          type="text"
          id="username-input"
          class="input"
          v-model="username"
        />
        <h4>
          <span v-if="this.$store.getters.languageGet">密码</span
          ><span v-else>Password</span>
        </h4>
        <input
          type="password"
          id="password-input"
          class="input"
          v-model="password"
        />
        <button @click="login">
          <span v-if="this.$store.getters.languageGet">登录</span
          ><span v-else>Log In</span>
        </button>
        <p>{{ loginStatus }}</p>
      </div>
      <div></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "navigation-desktop",
  data() {
    return {
      show: true,
      username: "",
      password: "",
      loginStatus: "",
      active: {
        color: "#bb9457ff",
        fontWeight: "bold",
      },
      home: {},
      bio: {},
      portfolio: {},
      contact: {},
    };
  },
  methods: {
    goToLanding: function () {
      setTimeout(() => {
        this.$router.push("/");
      }, 500);
    },
    goToHome: function () {
      setTimeout(() => {
        this.$router.push("/home");
      }, 1000);
    },
    goToBio: function () {
      setTimeout(() => {
        this.$router.push("/bio");
      }, 1000);
    },
    goToPortfolio: function () {
      this.$store.dispatch("getAllArtworks");
      setTimeout(() => {
        this.$router.push("/portfolio");
      }, 1000);
    },
    goToContact: function () {
      setTimeout(() => {
        this.$router.push("/contact");
      }, 1000);
    },
    showInput: function () {
      this.show = !this.show;
    },
    login: function () {
      if (this.username == "daisy0905" && this.password == "felix1101") {
        this.loginStatus = "Login Success!";
        setTimeout(() => {
          this.$router.push("/artworkoverview");
        }, 1000);
      } else {
        this.loginStatus = "Login Failed!";
      }
    },
  },
  mounted() {
    if (this.$router.history.current.path == "/home") {
      this.home = this.active;
    } else if (this.$router.history.current.path == "/bio") {
      this.bio = this.active;
    } else if (this.$router.history.current.path == "/portfolio") {
      this.portfolio = this.active;
    } else if (this.$router.history.current.path == "/contact") {
      this.contact = this.active;
    }
  },
};
</script>

<style lang="scss" scoped>
#nav {
  height: 12vh;
  width: 100%;
  display: grid;
  align-items: center;
  padding: 10px 0 0 0;
  margin-bottom: 1em;
  z-index: 100;
  margin-bottom: 0.5em;
}

#header {
  height: 100%;
  width: 100%;
  display: grid;
  grid-template-columns: 30% repeat(5, 10%) auto;
  justify-items: center;
  align-items: center;
  border-bottom: 1px solid darkgrey;

  h2 {
    font-weight: bold;
    font-size: 2rem;
    letter-spacing: 5px;
  }

  h3 {
    font-weight: bold;
    font-size: 1rem;
    margin-left: 2em;
    color: black;

    &:hover {
      cursor: pointer;
      border-bottom: 2px solid #bb9457ff;
    }

    &:active {
      color: #bb9457ff;
      border-bottom: 2px solid #6f1d1bff;
    }
  }

  #login-btn {
    width: 50%;
    height: 4vh;
    font-size: 0.8rem;
    border: 1px solid black;
    box-shadow: 1px 1px 2px grey;
    font-weight: bold;
    margin-right: 2em;
  }
}
#login {
  width: 100%;
  height: 100%;
  display: grid;
  justify-items: right;
  align-items: right;
  margin-right: 1em;
  grid-template-columns: 60% 35% 5%;
  z-index: 100;

  #form {
    width: 40%;
    height: 90%;
    display: grid;
    justify-items: right;
    align-items: right;

    h4 {
      font-size: 0.8rem;
      margin: 0.5em 0 0.5em 0;
      color: black;
      font-weight: normal;
    }

    .input {
      width: 70%;
      height: 2vh;
      background-color: none;
      border: none;
      border-bottom: 1px solid black;
      margin: 0 0 0.5em 0;
      text-align: center;
    }

    button {
      width: 70%;
      height: 3vh;
      font-size: 0.8rem;
      border: 1px solid black;
      box-shadow: none;
      margin: 0.5em 0 0 0;
    }

    p {
      font-size: 0.6rem;
      margin: 1em 0 0.5em 0;
      text-align: center;
      color: black;
    }
  }
}
</style>