<template>
  <div id="nav">
    <div id="header">
      <div></div>
      <h3 @click="goToLanding">KEMIN TONG</h3>
      <div class="icon">
        <img
          v-if="display"
          @click="displayNavBar"
          src="../assets/hamburger-menu-icon.png"
          alt="nav icon"
        />
        <img
          v-else
          @click="hideNavBar"
          src="../assets/hamburger-menu-icon-open.png"
          alt="nav icon"
        />
      </div>
    </div>
    <div v-if="display == false" id="nav-bar">
      <div id="nav-unit-1">
        <div></div>
        <h4 :style="home" @click="goToHome">
          <span v-if="this.$store.getters.languageGet">首页</span
          ><span v-else>HOME</span>
        </h4>
        <h4 :style="bio" @click="goToBio">
          <span v-if="this.$store.getters.languageGet">个人简介</span
          ><span v-else>BIO</span>
        </h4>
        <h4 :style="portfolio" @click="goToPortfolio">
          <span v-if="this.$store.getters.languageGet">作品集</span
          ><span v-else>PORTFOLIO</span>
        </h4>
        <h4 :style="contact" @click="goToContact">
          <span v-if="this.$store.getters.languageGet">与我联系</span
          ><span v-else>CONTACT</span>
        </h4>
        <div></div>
      </div>
      <div id="nav-unit-2">
        <h4 id="login-btn" @click="showInput">
          <span v-if="this.$store.getters.languageGet">管理员登录</span
          ><span v-else>admin login</span>
        </h4>
        <div v-if="show == false" id="login">
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
          <h4 @click="login">
            <span v-if="this.$store.getters.languageGet">登录</span
            ><span v-else>Log In</span>
          </h4>
          <p>{{ loginStatus }}</p>
          <div></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "navigation",
  data() {
    return {
      display: true,
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
    displayNavBar: function () {
      this.display = false;
    },
    hideNavBar: function () {
      this.display = true;
    },
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
  height: 8vh;
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
  grid-template-columns: 10% 70% 20%;
  justify-items: center;
  align-items: center;
  border-bottom: 1px solid darkgrey;

  .icon {
    height: 100%;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: center;

    img {
      height: 25px;
      object-fit: cover;
    }
  }

  h3 {
    font-weight: bold;
    font-size: 1rem;
    letter-spacing: 0.5em;

    &:hover, &:active {
      cursor: pointer;
    }
  }
}

#nav-bar {
  min-height: 22vh;
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  justify-items: left;
  align-items: left;
  position: absolute;
  top: 14vh;
  background-color: black;
  opacity: 0.8;
  z-index: 100;

  #nav-unit-1 {
    height: 100%;
    width: 100%;
    display: grid;
    justify-items: left;
    align-items: left;
    row-gap: 1em;
  }

  h4 {
    font-weight: bold;
    font-size: 0.8rem;
    margin-left: 2em;
    color: white;
    letter-spacing: 0.2em;

    &:hover {
      cursor: pointer;
      border-bottom: 2px solid #bb9457ff;
    }

    &:active {
      color: #bb9457ff;
      border-bottom: 2px solid white;
    }
  }

  #nav-unit-2 {
    width: 100%;
    height: 8vh;
    display: grid;
    justify-items: right;
    align-items: center;
    margin-top: 1em;

    #login-btn {
      width: 55%;
      height: 3vh;
      font-size: 0.8rem;
      border: 1px solid white;
      box-shadow: 1px 1px 2px grey;
      font-weight: bold;
      margin: 0 2em 0.5em 0;
    }

    #login {
      width: 75%;
      display: grid;
      justify-items: right;
      align-items: center;
      margin-right: 1.6em;

      h5 {
        font-size: 0.6rem;
        margin-bottom: 0.2em;
        color: white;
        font-weight: normal;
      }

      .input {
        width: 75%;
        height: 2.5vh;
        background-color: none;
        border: none;
        border-bottom: 1px solid black;
        margin: 0 0 0.5em 0;
        text-align: center;
      }

      h4 {
        width: 75%;
        height: 3vh;
        font-size: 0.8rem;
        border: 1px solid grey;
        box-shadow: none;
        margin: 0.2em 0 0 0;
        font-weight: normal;
      }

      p {
        font-size: 0.6rem;
        margin: 0.5em 0 0.5em 0;
        text-align: center;
        color: white;
      }
    }
  }
}

@media only screen and (min-width: 600px) {
  #header {
    .icon {
      height: 100%;
      width: 100%;
      display: grid;
      justify-items: center;
      align-items: center;

      img {
        height: 30px;
      }
    }

    h3 {
      font-size: 1.5rem;
    }
  }

  #nav-bar {
    top: 14vh;

    h2 {
      font-size: 1.2rem;
    }

    #nav-unit-2 {
      #login-btn {
        width: 42%;
        font-size: 1rem;
        margin-right: 2.5em;
      }

      #login {
        width: 60%;
        margin-right: 2.5em;

        h4 {
          font-size: 1rem;
        }

        button {
          font-size: 1rem;
        }

        p {
          font-size: 1rem;
        }
      }
    }
  }
}
</style>