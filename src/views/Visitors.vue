<template>
  <div id="visitors">
    <div v-if="login == undefined" id="login-check">
      <img @click="exit" src="../assets/exit-icon.png" alt="exit icon" />
      <h3>Sorry, You Have No Authorization To Visiting This Webpage!</h3>
      <h3>抱歉，您没有权限访问此页面！</h3>
    </div>
    <div v-if="login" id="container">
      <navigation id="nav"></navigation>
      <nav-desktop id="nav-desktop"></nav-desktop>
      <div id="en-ch">
        <div></div>
        <h4 id="english" @click="showEnglish">EN</h4>
        <h4 id="chinese" @click="showChinese">中文</h4>
        <div></div>
      </div>
      <visitor-list></visitor-list>
      <div id="go-to-top">
        <a href="#visitors">TO TOP</a>
      </div>
    </div>
    <footer-contact></footer-contact>
  </div>
</template>

<script>
import Navigation from "../components/Nav.vue";
import VisitorList from "../components/VisitorList.vue";
import NavDesktop from "../components/NavDesktop.vue";
import FooterContact from "../components/FooterContact.vue";
import cookies from "vue-cookies";

export default {
  components: {
    Navigation,
    VisitorList,
    NavDesktop,
    FooterContact,
  },
  data() {
    return {
      open: false,
      login: cookies.get("login"),
    };
  },
  methods: {
    showEnglish: function () {
      cookies.remove("chinese");
      this.$store.commit("updateLanguage", false);
      document.getElementById("english").style.color = "#bb9457ff";
      document.getElementById("chinese").style.color = "black";
    },
    showChinese: function () {
      cookies.set("chinese", true);
      this.$store.commit("updateLanguage", true);
      document.getElementById("chinese").style.color = "#bb9457ff";
      document.getElementById("english").style.color = "black";
    },
  },
  mounted() {
    this.showEnglish();
  },
  exit: function () {
    this.$router.push("/");
  },
};
</script>

<style lang="scss" scoped>
#visitors {
  width: 100%;
  display: grid;
  align-items: start;
}

#login-check {
  width: 100%;
  height: 100vh;
  display: grid;
  justify-items: center;
  align-items: center;
  align-content: start;
  background-attachment: fixed;
  background-repeat: no-repeat;
  background: url(../assets/bio_background_mobile.jpg);
  background-size: cover;
  background-position: center;

  img {
    width: 30px;
    height: 30px;
    margin-top: 1em;

    &:hover, &:active {
      cursor: pointer;
    }
  }

  h3 {
    width: 90%;
    font-weight: bold;
    font-size: 1rem;
    padding: 10em 0 5em 0;
  }
}

#container {
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: start;
}

#nav {
  height: 3em;
  width: 100%;
}

#nav-desktop {
  display: none;
}

#en-ch {
  height: 5vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
  grid-template-columns: 40% 10% 10% 40%;
  background-color: lightgrey;

  h4 {
    font-weight: bold;
    font-size: 0.8rem;

    &:hover,
    &:active {
      cursor: pointer;
    }
  }
}

#go-to-top {
  position: fixed;
  bottom: 22vh;
  right: 3vw;
  width: 5vw;
  height: 5vh;
  display: grid;
  align-items: center;
  justify-items: center;
  z-index: 20;

  a {
    color: white;
    width: 100%;
    padding: 0.6em;
    box-shadow: 1px 1px 2px black;
    opacity: 1;
    font-size: 0.6rem;

    &:link,
    &:visited {
      background-color: black;
    }

    &:hover,
    &:active {
      background-color: grey;
    }
  }
}

@media only screen and (min-width: 600px) {
  #login-check {

    img {
      width: 40px;
      height: 40px;
      margin-top: 2em;
    }

    h3 {
      width: 70%;
      font-size: 1.5rem;
      padding: 8em 0 5em 0;
      line-height: 1.5em;
    }
  }

  #nav {
    height: 4.5em;
  }

  #en-ch {
    h4 {
      font-size: 1.2rem;
    }
  }

  #go-to-top {
    bottom: 22vh;
    right: 1vw;
    width: 5vw;
    height: 10vh;

    a {
      font-size: 0.8rem;
    }
  }
}

@media only screen and (min-width: 1024px) {
  #login-check {

    h3 {
      width: 70%;
      font-size: 1.2rem;
      padding: 5em 0 5em 0;
    }
  }

  #nav {
    display: none;
  }

  #nav-desktop {
    width: 100%;
    height: 5em;
    display: grid;
    justify-items: center;
    align-items: center;
  }

  #en-ch {
    height: 5em;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: center;
    grid-template-columns: 5% 10% 10% auto;
    background-color: white;
    margin-left: 1em;

    h4 {
      font-weight: bold;
      font-size: 1rem;
    }
  }

  #go-to-top {
    bottom: 22vh;
    right: 1vw;
    width: 5vw;
    height: 10vh;

    a {
      font-size: 0.8rem;
    }
  }
}
</style>