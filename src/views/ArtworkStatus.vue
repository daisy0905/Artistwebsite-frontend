<template>
  <div id="status-list">
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
      <div id="container-1">
        <div class="art-status">
          <div></div>
          <h4>{{ availableNum }}</h4>
          <h4 id="availableStatus" @click="getAvailable">
            <span v-if="this.$store.getters.languageGet">在库</span
            ><span v-else>Available</span>
          </h4>
          <div></div>
        </div>
        <div class="art-status">
          <div></div>
          <h4>{{ onholdNum }}</h4>
          <h4 id="onHoldStatus" @click="getOnhold">
            <span v-if="this.$store.getters.languageGet">已预订</span
            ><span v-else>On hold</span>
          </h4>
          <div></div>
        </div>
        <div class="art-status">
          <div></div>
          <h4>{{ soldNum }}</h4>
          <h4 id="soldStatus" @click="getSold">
            <span v-if="this.$store.getters.languageGet">已售</span
            ><span v-else>Sold</span>
          </h4>
          <div></div>
        </div>
      </div>
      <status class="status" :Status="status"></status>
      <div id="go-to-top">
        <a href="#status-list">TO TOP</a>
      </div>
    </div>
    <footer-contact></footer-contact>
  </div>
</template>

<script>
import Navigation from "../components/Nav.vue";
import NavDesktop from "../components/NavDesktop.vue";
import FooterContact from "../components/FooterContact.vue";
import cookies from "vue-cookies";
import Status from "../components/Status.vue";

export default {
  components: {
    Navigation,
    NavDesktop,
    FooterContact,
    Status,
  },
  data() {
    return {
      status: "available",
      login: cookies.get("login"),
    };
  },
  props: {
    Status: {
      type: String,
    },
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
    getAvailable: function () {
      this.status = "available";
      document.getElementById("availableStatus").style.color = "#bb9457ff";
      document.getElementById("onHoldStatus").style.color = "black";
      document.getElementById("soldStatus").style.color = "black";
    },
    getOnhold: function () {
      this.status = "onhold";
      document.getElementById("availableStatus").style.color = "black";
      document.getElementById("onHoldStatus").style.color = "#bb9457ff";
      document.getElementById("soldStatus").style.color = "black";
    },
    getSold: function () {
      this.status = "sold";
      document.getElementById("availableStatus").style.color = "black";
      document.getElementById("onHoldStatus").style.color = "black";
      document.getElementById("soldStatus").style.color = "#bb9457ff";
    },
    exit: function () {
      this.$router.push("/");
    },
  },
  mounted() {
    if (this.$store.state.artworks.length == 0) {
      this.$store.dispatch("getAllArtworks");
    }
    this.showEnglish();
    this.getAvailable();
  },
  computed: {
    availableNum() {
      console.log(this.$store.getters.getAvailable);
      return this.$store.getters.getAvailable.length;
    },
    onholdNum() {
      console.log(this.$store.getters.getOnhold);
      return this.$store.getters.getOnhold.length;
    },
    soldNum() {
      console.log(this.$store.getters.getSold);
      return this.$store.getters.getSold.length;
    },
  },
};
</script>

<style lang="scss" scoped>
#status-list {
  min-height: 30vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: left;
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
    font-family: Arial, Helvetica, sans-serif;
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
    margin: 0;
  }
}

#container-1 {
  height: 5vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: start;
  grid-template-columns: 1fr 1fr 1fr;

  .art-status {
    height: 5vh;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: start;
    grid-template-columns: 1fr 1fr 2.5fr 1fr;
    margin-top: 1em;

    h4 {
      font-weight: bold;
      font-size: 0.8rem;

      &:hover, &:active {
        cursor: pointer;
      }
    }
  }
}

.status {
  min-height: 80vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: start;
  align-content: start;
}

#go-to-top {
  position: fixed;
  bottom: 22vh;
  right: 2vw;
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

  #nav-desktop {
    display: none;
  }

  #en-ch {
    h4 {
      font-size: 1.2rem;
    }
  }

  #container-1 {
    .art-status {
      h4 {
        font-size: 1.2rem;
      }
    }
  }

  .status {
    width: 100%;
    grid-template-columns: 1fr 1fr;
  }

  #go-to-top {
    bottom: 22vh;
    right: 0;
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
    height: 10vh;
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

  #container-1 {
    height: 6vh;
    width: 100%;
    background-color: lightgrey;
    column-gap: 0.5em;
    justify-items: center;
    align-items: center;
    margin-top: 0.5em;

    .art-status {
      height: 100%;
      width: 100%;
      display: grid;
      justify-items: center;
      align-items: center;
      grid-template-columns: 1fr 1fr 2.5fr 1fr;
      margin-top: 0;

      h4 {
        font-size: 1rem;
      }
    }
  }

  .status {
    min-height: 70vh;
    grid-template-columns: 1fr 1fr 1fr;
    margin-top: 1em;
  }

  #go-to-top {
    bottom: 22vh;
    right: 0;
    width: 5vw;
    height: 10vh;

    a {
      font-size: 1rem;
    }
  }
}
</style>