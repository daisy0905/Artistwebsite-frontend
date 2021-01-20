<template>
  <div id="home">
    <navigation id="nav-en"></navigation>
    <nav-desktop id="nav-desktop"></nav-desktop>
    <div id="en-ch">
      <div></div>
      <h4 id="english" @click="showEnglish">EN</h4>
      <h4 id="chinese" @click="showChinese">中文</h4>
      <div></div>
    </div>
    <div id="content">
      <img src="../assets/artist.png" alt="artist's portrait" />
      <div></div>
    </div>
    <div class="text">
      <h1><span v-if="this.$store.getters.languageGet">油画艺术家</span><span v-else>OIL PAINTING ARTIST</span></h1>
      <h1><span v-if="this.$store.getters.languageGet">童柯敏</span><span v-else>TONG, KEMIN</span></h1>
    </div>
    <footer-section></footer-section>
  </div>
</template>

<script>
import FooterSection from '../components/Footer.vue'
import Navigation from "../components/Nav.vue"
import NavDesktop from '../components/NavDesktop.vue'
import cookies from "vue-cookies"
export default {
  components: {
    Navigation,
    NavDesktop,
    FooterSection
  },
  data() {
    return {
        firstname: "",
        lastname: "",
        email: "",
    }
  }, 
  methods: {
    showEnglish: function () {
      cookies.remove("chinese")
      this.$store.commit("updateLanguage", false)
      console.log(this.$store.getters.languageGet)
      document.getElementById("english").style.color = "#bb9457ff";
      document.getElementById("chinese").style.color = "black";
    },
    showChinese: function () {
      cookies.set("chinese", true)
      this.$store.commit("updateLanguage", true)
      console.log(this.$store.getters.languageGet)
      document.getElementById("english").style.color = "black";
      document.getElementById("chinese").style.color = "#bb9457ff";
    },
  },
  mounted () {
            this.showEnglish();
        }
};
</script>

<style lang="scss" scoped>
#home {
  height: 100vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
}

#nav-en {
  height: 8vh;
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
    
    &:hover, &:active {
      cursor: pointer;
    }
  }
}

#content {
  height: 92vh;
  width: 100%;

  img {
    width: 100%;
    height: 92vh;
    object-fit: cover;
    margin-top: 0.3em;
  }
}

.text {
  position: absolute;
  width: 80%;
  height: 5vh;
  top: 55vh;
  left: 13vw;
  display: grid;
  justify-items: center;
  align-items: center;

  h1 {
    font-size: 1.8rem;
    color: white;
    text-align: center;
    padding: 0.5em;
    letter-spacing: 5px;
    text-shadow: 2px 2px 2px black;
    font-weight: bold;
  }
}

@media only screen and (min-width: 600px) {
#nav-desktop {
  display: none;
}

#en-ch {

  h4 {
    font-size: 1.2rem;
  }
}

#content {
  

  img {
    margin-top: 0.6em;
  }
}

.text {

  h1 {
    font-size: 2.5rem;
    letter-spacing: 0.5em;
  }
}

}

@media only screen and (min-width: 1024px) {
#home {
  min-height: 50vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
}

#nav-en {
  display: none;
}

#nav-ch {
  display: none;
}

#nav-desktop {
  width: 100%;
  height: 12vh;
  display: grid;
  justify-items: center;
  align-items: center;
}

#en-ch {
  height: 13vh;
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

#content {
  min-height: 50vh;
  width: 100%;
  display: grid;
  background-attachment: fixed; 
  background-repeat: no-repeat;
  background: url(../assets/background-image-1.jpg);
  background-size: cover;
  background-position: center;
  grid-template-columns: 40% 60%;

  img {
    width: 100%;
    object-fit: cover;
    margin-top: 0;
    filter: grayscale(100%);
  }
}

.text {
  position: absolute;
  width: 70%;
  height: 5vh;
  top: 60vh;
  left: 35vw;
  display: grid;
  justify-items: center;
  align-items: center;

  h1 {
    font-size: 1.8rem;
    color: white;
    text-align: center;
    padding: 0;
    letter-spacing: 8px;
    text-shadow: 2px 2px 2px black;
    font-weight: bold;
    line-height: 1.5em;
  }
}
}
</style>
