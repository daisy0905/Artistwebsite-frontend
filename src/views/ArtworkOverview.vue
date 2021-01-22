<template>
  <div id="artwork-list">
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
      <artwork-card-list class="artworks"></artwork-card-list>
      <div id="upload-artwork">
        <img
          @click="openUpload"
          src="../assets/upload-icon.png"
          alt="artwork upload icon"
        />
      </div>
      <upload-form class="upload-form" v-if="open"></upload-form>
      <div id="go-to-top">
        <a href="#artwork-list">TO TOP</a>
      </div>
    </div>
    <footer-contact></footer-contact>
  </div>
</template>

<script>
import ArtworkCardList from "../components/ArtworkCardList.vue";
import FooterContact from "../components/FooterContact.vue";
import Navigation from "../components/Nav.vue";
import NavDesktop from "../components/NavDesktop.vue";
import UploadForm from "../components/UploadForm.vue";
import cookies from "vue-cookies";

export default {
  components: {
    Navigation,
    ArtworkCardList,
    NavDesktop,
    UploadForm,
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
    openUpload: function () {
      this.open = !this.open;
    },
    exit: function () {
      this.$router.push("/");
    },
  },
  mounted() {
    this.showEnglish();
  },
};
</script>

<style lang="scss" scoped>
#artwork-list {
  min-height: 100vh;
  width: 100%;
  display: grid;
  justify-items: center;
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
    font-family: Arial, Helvetica, sans-serif;
    font-size: 0.8rem;
    margin: 0;
  }
}

.artworks {
  min-height: 100vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
  margin-top: 1em;
  row-gap: 1vh;
}

#upload-artwork {
  position: fixed;
  left: 0;
  bottom: 20vh;
  z-index: 1000;

  img {
    height: 30px;
    width: 30px;

    &:hover,
    &:active {
      cursor: pointer;
    }
  }
}

.upload-form {
  position: fixed;
  min-height: 100vh;
  width: 100%;
  left: 0;
  bottom: 0;
  z-index: 500;
  background-attachment: fixed;
  background-repeat: no-repeat;
  background: url(../assets/artwork_background.jpg);
  background-size: cover;
  background-position: center;
  box-shadow: 4px 4px 4px grey;
}

#go-to-top {
  position: fixed;
  bottom: 20vh;
  right: 0;
  width: 10vw;
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

  #upload-artwork {
    img {
      height: 50px;
      width: 50px;
    }
  }

  .upload-form {
    height: 70vh;
    width: 80%;
  }

  #go-to-top {
    width: 5vw;
    height: 10vh;

    a {
      font-size: 0.8rem;
    }
  }
}

@media only screen and (min-width: 1024px) {
  #artwork-list {
    min-height: 100vh;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: start;
  }

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

  .artworks {
    min-height: 100vh;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: start;
    row-gap: 1vh;
    grid-template-columns: 1fr 1fr;
  }

  .upload-form {
    height: 100vh;
    width: 40%;
    left: 2vw;
    bottom: 0;
  }

  #go-to-top {
    right: 0;
    width: 2.5vw;
    height: 10vh;

    a {
      font-size: 0.8rem;
    }
  }
}
</style>