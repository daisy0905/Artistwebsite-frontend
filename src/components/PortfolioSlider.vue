<template>
  <div id="cover-image">
    <div class="container">
      <div class="slider-icon">
        <a class="icon" @click="prevL" href="#/portfolio">&#10094;</a>
        <h2>
          <span v-if="this.$store.getters.languageGet">风景</span
          ><span v-else>LANDSCAPE</span>
        </h2>
        <a class="icon" @click="nextL" href="#/portfolio">&#10095;</a>
      </div>
      <div class="main-image" v-for="i in [currentIndex]" :key="i">
        <img :src="mainImageSrcL" />
      </div>
      <div class="slider-button">
        <button @click="getArtwork">
          <span v-if="this.$store.getters.languageGet">详情</span
          ><span v-else>DETAILS</span>
        </button>
      </div>
    </div>
    <div class="container">
      <div class="slider-icon">
        <a class="icon" @click="prevP" href="#/portfolio">&#10094;</a>
        <h2>
          <span v-if="this.$store.getters.languageGet">人物</span
          ><span v-else>PORTRAIT</span>
        </h2>
        <a class="icon" @click="nextP" href="#/portfolio">&#10095;</a>
      </div>
      <div class="main-image" v-for="i in [currentIndex]" :key="i">
        <img :src="mainImageSrcP" />
      </div>
      <div class="slider-button">
        <button @click="getArtwork">
          <span v-if="this.$store.getters.languageGet">详情</span
          ><span v-else>DETAILS</span>
        </button>
      </div>
    </div>
    <div class="container">
      <div class="slider-icon">
        <a class="icon" @click="prevO" href="#/portfolio">&#10094;</a>
        <h2>
          <span v-if="this.$store.getters.languageGet">其它</span
          ><span v-else>OTHERS</span>
        </h2>
        <a class="icon" @click="nextO" href="#/portfolio">&#10095;</a>
      </div>
      <div class="main-image" v-for="i in [currentIndex]" :key="i">
        <img :src="mainImageSrcO" />
      </div>
      <div class="slider-button">
        <button @click="getArtwork">
          <span v-if="this.$store.getters.languageGet">详情</span
          ><span v-else>DETAILS</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
// import axios from "axios"
import cookies from "vue-cookies";
export default {
  data() {
    return {
      currentIndex: 0,
      mainImageSrcL: "",
      mainImageSrcP: "",
      mainImageSrcO: "",
      id: "",
    };
  },
  computed: {
    imagesL() {
      console.log(this.$store.getters.getLandscape);
      if (this.$store.getters.getLandscape == []) return;
      return this.$store.getters.getLandscape;
    },
    imagesP() {
      console.log(this.$store.getters.getPortrait);
      if (this.$store.getters.getPortrait == undefined) return;
      return this.$store.getters.getPortrait;
    },
    imagesO() {
      console.log(this.$store.getters.getOther);
      if (this.$store.getters.getOther == undefined) return;
      return this.$store.getters.getOther;
    },
  },
  methods: {
    nextL: function () {
      this.mainImageSrcL = this.imagesL[
        Math.abs(this.currentIndex++) % this.imagesL.length
      ].url;
      this.getIdL();
      console.log(this.id);
    },
    prevL: function () {
      this.mainImageSrcL = this.imagesL[
        Math.abs(this.currentIndex--) % this.imagesL.length
      ].url;
      this.getIdL();
      console.log(this.id);
    },
    createdL: function () {
      if (
        this.imagesL[Math.abs(this.currentIndex) % this.imagesL.length] ==
        undefined
      )
        return;
      this.mainImageSrcL = this.imagesL[
        Math.abs(this.currentIndex) % this.imagesL.length
      ].url;
    },
    getIdL: function () {
      for (let i = 0; i < this.imagesL.length; i++) {
        if (this.mainImageSrcL == this.imagesL[i].url) {
          this.id = this.imagesL[i].id;
        }
      }
      cookies.set("id", this.id);
      return this.id;
    },
    nextP: function () {
      this.mainImageSrcP = this.imagesP[
        Math.abs(this.currentIndex++) % this.imagesP.length
      ].url;
      this.getIdP();
      console.log(this.id);
    },
    prevP: function () {
      this.mainImageSrcP = this.imagesP[
        Math.abs(this.currentIndex--) % this.imagesP.length
      ].url;
      this.getIdP();
      console.log(this.id);
    },
    createdP: function () {
      if (
        this.imagesP[Math.abs(this.currentIndex) % this.imagesP.length] ==
        undefined
      )
        return;
      this.mainImageSrcP = this.imagesP[
        Math.abs(this.currentIndex) % this.imagesP.length
      ].url;
    },
    getIdP: function () {
      for (let j = 0; j < this.imagesP.length; j++) {
        if (this.mainImageSrcP == this.imagesP[j].url) {
          this.id = this.imagesP[j].id;
        }
      }
      cookies.set("id", this.id);
      return this.id;
    },
    nextO: function () {
      this.mainImageSrcO = this.imagesO[
        Math.abs(this.currentIndex++) % this.imagesO.length
      ].url;
      this.getIdO();
      console.log(this.id);
    },
    prevO: function () {
      this.mainImageSrcO = this.imagesO[
        Math.abs(this.currentIndex--) % this.imagesO.length
      ].url;
      this.getIdO();
      console.log(this.id);
    },
    createdO: function () {
      if (
        this.imagesO[Math.abs(this.currentIndex) % this.imagesO.length] ==
        undefined
      )
        return;
      this.mainImageSrcO = this.imagesO[
        Math.abs(this.currentIndex) % this.imagesO.length
      ].url;
    },
    getIdO: function () {
      for (let k = 0; k < this.imagesO.length; k++) {
        if (this.mainImageSrcO == this.imagesO[k].url) {
          this.id = this.imagesO[k].id;
        }
      }
      cookies.set("id", this.id);
      return this.id;
    },
    getArtwork: function () {
      this.$store.dispatch("getArtwork");
      setTimeout(() => {
        this.$router.push("/artwork");
      }, 1000);
    },
  },
  mounted() {
    setTimeout(() => {
      this.createdL();
      this.createdP();
      this.createdO();
    }, 300);
  },
};
</script>

<style lang="scss" scoped>
#cover-image {
  min-height: 50vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
  row-gap: 0.2em;
}

.container {
  height: 50vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
  position: relative;

  .slider-icon {
    height: 6vh;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: center;
    grid-template-columns: 40% 20% 40%;
    position: absolute;
    z-index: 100;
    opacity: 0.8;

    .icon {
      color: white;
      text-decoration: none;
      font-size: 2.5rem;
    }

    h2 {
      font-weight: bold;
      font-size: 1.2rem;
      color: white;
      text-align: center;
      text-shadow: 1px 1px 2px black;
    }
  }

  .main-image {
    height: 50vh;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: center;

    img {
      height: 100%;
      width: 100%;
      object-fit: cover;
    }
  }

  .slider-button {
    width: 100%;
    height: 5vh;
    display: grid;
    justify-items: center;
    align-items: center;
    position: absolute;
    top: 30vh;

    button {
      width: 40%;
      height: 100%;
      font-size: 1rem;
      color: white;
      background-color: transparent;
      border: none;
      border-top: 1px solid white;
      border-bottom: 1px solid white;
    }
  }
}

@media only screen and (min-width: 600px) {
  #cover-image {
    #slider-icon {
      .icon {
        font-size: 2rem;
      }
    }

    #main-image {
      height: 50vh;
      width: 100%;
      display: grid;
      justify-items: center;
      align-items: center;

      img {
        height: 100%;
        width: 100%;
        object-fit: cover;
      }
    }
  }
}

@media only screen and (min-width: 1024px) {
  #cover-image {
    height: 60vh;
    #slider-icon {
      .icon {
        font-size: 2rem;
      }
    }

    #main-image {
      height: 100%;
    }
  }
}
</style>
