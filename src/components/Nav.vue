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
    <div v-if="nav">
      <div v-if="display == false" class="nav-bar">
        <div class="nav-unit-1">
          <div></div>
          <h4 :style="artworkoverview" @click="goToArtworkOverview">
            <span v-if="this.$store.getters.languageGet">作品总览</span
            ><span v-else>ARTWORK OVERVIEW</span>
          </h4>
          <h4 :style="artworkstatus" @click="goToArtworkStatus">
            <span v-if="this.$store.getters.languageGet">作品状态</span
            ><span v-else>ARTWORK STATUS</span>
          </h4>
          <h4 :style="enquiry" @click="goToEnquiry">
            <span v-if="this.$store.getters.languageGet">留言总览</span
            ><span v-else>ENQUIRY REVIEW</span>
          </h4>
          <h4 :style="visitors" @click="goToVisitors">
            <span v-if="this.$store.getters.languageGet">访客清单</span
            ><span v-else>VISITOR LIST</span>
          </h4>
          <div></div>
        </div>
        <div class="nav-unit-2">
          <h4 class="login-btn" @click="showInput">
            <span v-if="this.$store.getters.languageGet">管理员退出</span
            ><span v-else>admin logout</span>
          </h4>
          <div v-if="show == false" class="login">
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
            <h4 @click="logout">
              <span v-if="this.$store.getters.languageGet">退出</span
              ><span v-else>Log Out</span>
            </h4>
            <p>{{ logoutStatus }}</p>
          </div>
          <div></div>
        </div>
      </div>
    </div>
    <div v-if="nav == undefined">
      <div v-if="display == false" class="nav-bar">
        <div class="nav-unit-1">
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
        <div class="nav-unit-2">
          <h4 class="login-btn" @click="showInput">
            <span v-if="this.$store.getters.languageGet">管理员登录</span
            ><span v-else>admin login</span>
          </h4>
          <div v-if="show == false" class="login">
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
  </div>
</template>

<script>
import cookies from "vue-cookies";
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
      artworkoverview: {},
      artworkstatus: {},
      enquiry: {},
      visitors: {},
      nav: cookies.get("login"),
      logoutStatus: "",
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
  align-items: center;
  padding: 10px 0 0 0;
  z-index: 100;
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

    &:hover,
    &:active {
      cursor: pointer;
    }
  }
}

.nav-bar {
  min-height: 24vh;
  width: 100%;
  display: grid;
  grid-template-columns: 1.2fr 1fr;
  justify-items: left;
  align-items: start;
  position: absolute;
  top: 13vh;
  left: 0;
  background-color: black;
  opacity: 0.8;
  z-index: 100;
}

.nav-unit-1 {
  height: 100%;
  width: 100%;
  display: grid;
  justify-items: left;
  align-items: start;
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

.nav-unit-2 {
  width: 100%;
  height: 8vh;
  display: grid;
  justify-items: right;
  align-items: start;
  margin-top: 1em;
}

.login-btn {
  width: 70%;
  height: 3vh;
  font-size: 0.8rem;
  border: 1px solid white;
  box-shadow: 1px 1px 2px grey;
  font-weight: bold;
  margin: 0 2em 0.5em 0;
}

.login {
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
    font-size: 0.8rem;
    text-align: center;
    color: white;
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

  h4 {
    font-size: 1.2rem;
  }

  .login-btn {
    width: 45%;
    font-size: 1.2rem;
    margin: 0.8em 2em 0.5em 0;
  }

  .login {
    h5 {
      font-size: 1rem;
    }

    .input {
      width: 60%;
    }

    h4 {
      width: 60%;
      font-size: 1.2rem;
    }

    p {
      font-size: 0.8rem;
    }
  }
}
</style>