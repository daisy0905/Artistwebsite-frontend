<template>
  <div id="bio">
    <navigation id="nav"></navigation>
    <nav-desktop id="nav-desktop"></nav-desktop>
    <div id="en-ch">
      <div></div>
      <h4 id="english" @click="showEnglish">EN</h4>
      <h4 id="chinese" @click="showChinese">中文</h4>
      <div></div>
    </div>
    <div id="content">
      <div id="unit-2">
        <img id="image" src="../assets/portrait.jpg" alt="artist's portrait" />
      </div>
      <div class="unit-3">
        <h2>
          <span v-if="this.$store.getters.languageGet">童柯敏</span
          ><span v-else>TONG, KEMIN</span>
        </h2>
        <h3>
          <span v-if="this.$store.getters.languageGet">职业油画家</span
          ><span v-else>PROFESSIONAL ARTIST</span>
        </h3>
        <p>
          <span v-if="this.$store.getters.languageGet">
            中国美术家协会会员、中国金融美术家协会主席团成员、湖南省美术家协会油画艺委会副主任、湖南省油画学会副秘书长、湖南省油画风景研究会副会长兼秘书长、湖南省当代油画院副院长、长沙市美术家协会副主席、湖南省金融美术家协会名誉主席、湘潭齐白石纪念馆特聘画家。
          </span>
          <span v-else>
            Member of the Chinese Artists Association, member of the Presidium
            of the China Financial Artists Association, Deputy Director of the
            Oil Painting Committee of the Hunan Artists Association, Deputy
            Secretary-General of the Hunan Oil Painting Society, Vice President
            and Secretary General of the Hunan Oil Painting Landscape Research
            Association, Hunan Contemporary Vice President of the Oil Painting
            Academy, Vice Chairman of Changsha Artists Association, Honorary
            Chairman of Hunan Financial Artists Association, Special Painter of
            Xiangtan Qi Baishi Memorial Hall.
          </span>
        </p>
      </div>
    </div>
    <footer-section></footer-section>
  </div>
</template>

<script>
import Navigation from "../components/Nav.vue";
import NavDesktop from "../components/NavDesktop.vue";
import FooterSection from "../components/Footer.vue";
import cookies from "vue-cookies";
export default {
  components: {
    Navigation,
    NavDesktop,
    FooterSection,
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
};
</script>

<style lang="scss" scoped>
#bio {
  min-height: 100vh;
  width: 100%;
  display: grid;
  align-items: center;
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

#content {
  min-height: 92vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
  margin-top: 0.5em;
  background-attachment: fixed;
  background-repeat: no-repeat;
  background: url(../assets/bio_background_mobile.jpg);
  background-size: cover;
  background-position: center;
  padding-bottom: 2em;

  #unit-2 {
    height: 35vh;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: start;
    margin-top: 2em;

    img {
      width: 200px;
      box-shadow: 8px 8px 2px grey;
      opacity: 0.9;
    }
  }

  .unit-3 {
    min-height: 35vh;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: center;
    margin-top: 4em;

    h2 {
      font-weight: bold;
      font-size: 1.5rem;
    }

    h3 {
      font-size: 1rem;
      margin-top: 0.5em;
    }

    p {
      width: 70%;
      min-height: 40vh;
      font-size: 0.8rem;
      text-align: justify;
      line-height: 1.5em;
      margin: 1em 0 1em 0;
    }
  }
}

@media only screen and (min-width: 600px) {
  #nav {
    height: 4.5em;
  }

  #bio {
    width: 100%;
    min-height: 30vh;
    display: grid;
    align-items: center;
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

  #content {
    min-height: 50vh;
    width: 100%;
    margin-top: 0.8em;

    #unit-2 {
      height: 40vh;
      width: 100%;
      display: grid;
      justify-items: center;
      align-items: center;
      padding-top: 3em;

      img {
        width: 350px;
      }
    }

    .unit-3 {
      margin-top: 7em;

      h2 {
        font-size: 1.8rem;
      }

      h3 {
        font-size: 1.2rem;
      }

      p {
        min-height: 30vh;
        width: 70%;
        font-size: 1.2rem;
        padding-bottom: 2em;
      }
    }
  }
}

@media only screen and (min-width: 1024px) {
  #bio {
    min-height: 80vh;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: center;
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

  #content {
    min-height: 30vh;
    margin-top: 0.3em;
    display: grid;
    align-items: start;
    grid-template-columns: 1fr 1fr;

    .unit-2 {
      align-items: start;
    }


    .unit-3 {
      width: 100%;
      padding: 1em 0 6em 0;
      h2 {
        font-size: 1.5rem;
      }

      h3 {
        font-size: 1.2rem;
      }

      p {
        width: 70%;
        font-size: 1rem;
        margin-top: 1em;
        font-weight: bold;
      }
    }
  }
}
</style>
