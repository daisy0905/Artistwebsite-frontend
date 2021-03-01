<template>
  <div id="nav">
    <div id="header">
      <h2 @click="goToLanding">KEMIN TONG</h2>
      <div></div>
      <div class="nav-container" v-if="nav == undefined">
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
        <h3 class="login-btn" @click="showInput">
          <span v-if="this.$store.getters.languageGet">管理员登录</span
          ><span v-else>admin login</span>
        </h3>
        <div v-if="show == false" class="login">
          <div class="form">
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
      <div v-if="nav" class="nav-container">
        <h3 :style="artworkoverview" @click="goToArtworkOverview">
          <span v-if="this.$store.getters.languageGet">作品总览</span
          ><span v-else>ARTWORKS</span>
        </h3>
        <h3 :style="artworkstatus" @click="goToArtworkStatus">
          <span v-if="this.$store.getters.languageGet">作品状态</span
          ><span v-else>STATUS</span>
        </h3>
        <h3 :style="enquiry" @click="goToEnquiry">
          <span v-if="this.$store.getters.languageGet">>留言总览</span
          ><span v-else>ENQUIRIES</span>
        </h3>
        <h3 :style="visitors" @click="goToVisitors">
          <span v-if="this.$store.getters.languageGet">访客清单</span
          ><span v-else>VISITORS</span>
        </h3>
        <h3 class="login-btn" @click="showInput">
          <span v-if="this.$store.getters.languageGet">管理员退出</span
          ><span v-else>admin logout</span>
        </h3>
        <div v-if="show == false" class="login">
          <div class="form">
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
            <h4 @click="logout">
              <span v-if="this.$store.getters.languageGet">退出</span
              ><span v-else>Log Out</span>
            </h4>
            <div></div>
            <p>{{ logoutStatus }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import cookies from "vue-cookies";
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
      artworkoverview: {},
      artworkstatus: {},
      enquiry: {},
      visitors: {},
      nav: cookies.get("login"),
      logoutStatus: "",
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
    goToArtworkOverview: function () {
      setTimeout(() => {
        this.$router.push("/artworkoverview");
      }, 1000);
    },
    goToArtworkStatus: function () {
      setTimeout(() => {
        this.$router.push("/artworkstatus");
      }, 1000);
    },
    goToEnquiry: function () {
      setTimeout(() => {
        this.$router.push("/enquiryreview");
      }, 1000);
    },
    goToVisitors: function () {
      setTimeout(() => {
        this.$router.push("/visitors");
      }, 1000);
    },
    showInput: function () {
      this.show = !this.show;
    },
    login: function () {
      if (this.username == "test" && this.password == "test123") {
        this.loginStatus = "Login Success!";
        cookies.set("login", true);
        setTimeout(() => {
          this.$router.push("/artworkoverview");
        }, 1000);
      } else {
        this.loginStatus = "Login Failed!";
      }
    },
    logout: function () {
      if (this.username == "test" && this.password == "test123") {
        this.logoutStatus = "Log Out Success!";
        cookies.remove("login");
        setTimeout(() => {
          this.$router.push("/");
        }, 1000);
      } else {
        this.logoutStatus = "Log Out Failed!";
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
    } else if (this.$router.history.current.path == "/artworkoverview") {
      this.artworkoverview = this.active;
    } else if (this.$router.history.current.path == "/artworkstatus") {
      this.artworkstatus = this.active;
    } else if (this.$router.history.current.path == "/enquiryreview") {
      this.enquiry = this.active;
    } else if (this.$router.history.current.path == "/visitors") {
      this.visitors = this.active;
    }
  },
};
</script>

<style lang="scss" scoped>
#nav {
  width: 100%;
  display: grid;
  align-items: start;
  justify-items: center;
  z-index: 100;
}

#header {
  height: 100%;
  width: 100%;
  display: grid;
  grid-template-columns: 25% 5% 70%;
  justify-items: center;
  align-items: start;
  border-bottom: 1px solid darkgrey;

  h2 {
    font-weight: bold;
    font-size: 2rem;
    letter-spacing: 5px;
    padding: 0.7em 0 0.5em 0;

    &:hover,
    &:active {
      cursor: pointer;
    }
  }

  .nav-container {
    width: 100%;
    height: 100%;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    justify-items: center;
    align-items: start;
    padding: 1.4em 0 0.5em 0;

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

  .login-btn {
    width: 45%;
    height: 2em;
    font-size: 0.8rem;
    border: 1px solid black;
    box-shadow: 1px 1px 2px grey;
    font-weight: bold;
    margin-right: 2em;
    padding: 0.2em 0 0.4em 0;
  }
}
.login {
  width: 80%;
  height: 100%;
  display: grid;
  justify-items: right;
  align-items: start;
  margin-right: 1em;
  z-index: 100;
  position: relative;

  .form {
    width: 100%;
    height: 6em;
    display: grid;
    justify-items: right;
    align-items: start;
    grid-template-columns: 0.5fr 1fr;
    position: absolute;
    right: -54vw;
    top: 1vh;
    background-color: white;
    padding: 0.3em;

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
      height: 1.5em;
      font-size: 0.8rem;
      border: 1px solid black;
      box-shadow: none;
      margin: 0.1em 0 0 0;
      padding: 0.1em 0.2em 0.1em 0.2em;

      &:hover,
      &:active {
        cursor: pointer;
      }
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