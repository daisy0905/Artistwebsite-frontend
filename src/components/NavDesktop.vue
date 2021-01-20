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
      <h3 id="login-btn" @click="showInput">
        <span v-if="this.$store.getters.languageGet">管理员登录</span
        ><span v-else>admin login</span>
      </h3>
    </div>
    <div v-if="show == false" id="login">
      <div id="form">
        <h5>
          <span v-if="this.$store.getters.languageGet">用户名</span
          ><span v-else>Username</span>
        </h5>
        <input
          type="text"
          id="username-input"
          class="input"
          v-model="username"
        />
        <h5>
          <span v-if="this.$store.getters.languageGet">密码</span
          ><span v-else>Password</span>
        </h5>
        <input
          type="password"
          id="password-input"
          class="input"
          v-model="password"
        />
        <div></div>
        <h4 @click="login">
          <span v-if="this.$store.getters.languageGet">登录</span
          ><span v-else>Log In</span>
        </h4>
        <div></div>
        <p>{{ loginStatus }}</p>
      </div>
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
      if (this.username == "test" && this.password == "test123") {
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
  grid-template-columns: 25% repeat(5, 12%) auto;
  justify-items: center;
  align-items: center;
  border-bottom: 1px solid darkgrey;

  h2 {
    font-weight: bold;
    font-size: 2rem;
    letter-spacing: 5px;

    &:hover,
    &:active {
      cursor: pointer;
    }
  }

  h3 {
    font-weight: bold;
    font-size: 1.2rem;
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
    width: 40%;
    height: 5vh;
    font-size: 0.8rem;
    border: 1px solid black;
    box-shadow: 1px 1px 2px grey;
    font-weight: bold;
    margin-right: 2em;
    padding: 0.2em 0 0.4em 0;
  }
}
#login {
  width: 40%;
  height: 100%;
  display: grid;
  justify-items: right;
  align-items: center;
  margin-right: 1em;
  z-index: 100;
  position: relative;

  #form {
    width: 40%;
    height: 12vh;
    display: grid;
    justify-items: right;
    align-items: center;
    grid-template-columns: 0.5fr 1fr;
    position: absolute;
    right: -26vw;
    top: 0;

    h5 {
      font-size: 0.8rem;
      margin: 0.2em 0 0.2em 0;
      color: black;
      font-weight: normal;
    }

    .input {
      width: 80%;
      height: 2vh;
      background-color: none;
      border: none;
      border-bottom: 1px solid black;
      margin: 0 0 0.2em 0;
      text-align: center;
      font-size: 0.8rem;
    }

    h4 {
      width: 80%;
      height: 4vh;
      font-size: 0.8rem;
      border: 1px solid black;
      box-shadow: none;
      margin: 0.1em 0 0 0;
      padding: 0.1em 0.4em 0.1em 0.4em;

      &:hover,
      &:active {
        cursor: pointer;
      }
    }

    p {
      font-size: 0.6rem;
      margin: 1em 0 0.5em 0;
      text-align: center;
      color: white;
    }
  }
}
</style>