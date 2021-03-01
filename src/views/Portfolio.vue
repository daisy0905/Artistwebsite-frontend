<template>
  <div id="portfolio">
    <navigation id="nav"></navigation>
    <nav-desktop id="nav-desktop"></nav-desktop>
    <div id="en-ch">
      <div></div>
      <h4 id="english" @click="showEnglish">EN</h4>
      <h4 id="chinese" @click="showChinese">中文</h4>
      <div></div>
    </div>
    <div id="text-container">
      <div id="text-unit-1">
        <h2>
          <span v-if="this.$store.getters.languageGet">风景</span
          ><span v-else>LANDSCAPE</span>
        </h2>
        <h2>
          <span v-if="this.$store.getters.languageGet">人物</span
          ><span v-else>PORTRAIT</span>
        </h2>
      </div>
      <div id="text-unit-2">
        <h2 id="text-3">
          <span v-if="this.$store.getters.languageGet">其它</span
          ><span v-else>OTHERS</span>
        </h2>
      </div>
    </div>
    <div id="artwork-container-1">
      <artwork-slider Cate="landscape"></artwork-slider>
      <artwork-slider Cate="portrait"></artwork-slider>
    </div>
    <div id="artwork-container-2">
      <div></div>
      <artwork-slider Cate="other"></artwork-slider>
      <div></div>
    </div> 
    <footer-section></footer-section>
  </div>
</template>

<script>
import Navigation from "../components/Nav.vue";
import NavDesktop from "../components/NavDesktop.vue";
import FooterSection from "../components/Footer.vue";
import cookies from "vue-cookies";
import ArtworkSlider from "../components/ArtworkSlider.vue";

export default {
  components: {
    Navigation,
    NavDesktop,
    FooterSection,
    ArtworkSlider,
  },
  props: {
    Cate: {
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
  },
  mounted() {
    if (this.$store.state.artworks.length == 0) {
      this.$store.dispatch("getAllArtworks");
    }
    this.showEnglish();
  },
};
</script>

<style lang="scss" scoped>
#portfolio {
  min-height: 50vh;
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
  height: 2em;
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

#text-container {
  width: 100%;
  margin-top: 0.5em;
  display: grid;
  justify-items: center;
  align-items: center;
  z-index: 50;
  position: relative;

  #text-unit-1 {
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: center;
    position: absolute;
    grid-template-rows: 1fr 1fr;
    row-gap: 47vh;
    top: 19vh;

    h2 {
      font-size: 1.5rem;
      color: white;
      text-shadow: 1px 1px 1px black;
    }
  }

  #text-unit-2 {
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: center;
    position: absolute;
    top: 122vh;

    h2 {
      font-size: 1.5rem;
      color: white;
      text-shadow: 1px 1px 1px black;
    }
  }
}

#artwork-container-1 {
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
}

#artwork-container-2 {
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
}

@media only screen and (min-width: 600px) {
  #nav {
    height: 4.5em;
  }

  #nav-desktop {
    display: none;
  }

  #en-ch {
    height: 3em;
    h4 {
      font-size: 1.2rem;
    }
  }

  #text-container {
    #text-unit-1 {
      row-gap: 49vh;
      top: 19vh;

      h2 {
        font-size: 1.8rem;
        text-shadow: 2px 2px 2px black;
      }
    }

    #text-unit-2 {
      top: 123vh;

      h2 {
        font-size: 1.8rem;
        text-shadow: 2px 2px 2px black;
      }
    }
  }
}

@media only screen and (min-width: 1024px) {
  #portfolio {
    min-height: 60vh;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: start;
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

  #text-container {
    width: 90%;
    margin-top: 0.5em;
    display: grid;
    justify-items: center;
    align-items: center;
    position: relative;

    #text-unit-1 {
      grid-template-columns: 1fr 1fr;
      top: 20vh;

      h2 {
        font-size: 1.5rem;
        letter-spacing: 0.2em;
      }
    }

    #text-unit-2 {
      top: 89vh;

      h2 {
        font-size: 1.5rem;
        letter-spacing: 0.2em;
      }
    }
  }

  #artwork-container-1 {
    width: 90%;
    grid-template-columns: 1fr 1fr;
    margin-bottom: 1em;
    column-gap: 1em;
  }

  #artwork-container-2 {
    width: 90%;
    grid-template-columns: 25% 50% 25%;
    margin-bottom: 1em;
  }
}
</style>
