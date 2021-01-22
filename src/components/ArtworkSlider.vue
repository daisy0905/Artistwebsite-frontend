<template>
  <div class="container">
    <div class="slider-icon">
      <a class="icon" @click="prev" href="#/portfolio">&#10094;</a>
      <div></div>
      <a class="icon" @click="next" href="#/portfolio">&#10095;</a>
    </div>
    <div class="main-image" v-for="i in [currentIndex]" :key="i">
      <img :src="mainImageSrc" />
    </div>
    <div class="slider-button">
      <h3 @click="getArtwork">
        <span v-if="this.$store.getters.languageGet">详情</span
        ><span v-else>DETAILS</span>
      </h3>
    </div>
  </div>
</template>
<script>
import cookies from "vue-cookies";
export default {
  data() {
    return {
      currentIndex: 0,
      mainImageSrc: "",
      id: "",
    };
  },
  props: {
    Cate: {
      type: String,
    },
  },
  methods: {
    next: function () {
      this.mainImageSrc = this.images[
        Math.abs(this.currentIndex++) % this.images.length
      ].url;
      this.getId();
      console.log(this.id);
    },
    prev: function () {
      this.mainImageSrc = this.images[
        Math.abs(this.currentIndex--) % this.images.length
      ].url;
      this.getId();
      console.log(this.id);
    },
    created: function () {
      if (
        this.images[Math.abs(this.currentIndex) % this.images.length] ==
        undefined
      )
        return;
      this.mainImageSrc = this.images[
        Math.abs(this.currentIndex) % this.images.length
      ].url;
    },
    getId: function () {
      for (let i = 0; i < this.images.length; i++) {
        if (this.mainImageSrc == this.images[i].url) {
          this.id = this.images[i].id;
        }
      }
      return this.id;
    },
    getArtwork: function () {
      cookies.set("id", this.id);
      this.$store.dispatch("getArtwork");
      setTimeout(() => {
        this.$router.push("/artwork");
      }, 1000);
    },
  },
  mounted() {
    if (this.Cate == "landscape") {
      this.images = this.$store.getters.getLandscape;
      console.log(this.images);
    } else if (this.Cate == "portrait") {
      this.images = this.$store.getters.getPortrait;
      console.log(this.images);
    } else if (this.Cate == "other") {
      this.images = this.$store.getters.getOther;
      console.log(this.images);
    }
    setTimeout(() => {
      this.created();
    }, 300);
  },
};
</script>

<style lang="scss" scoped>
.container {
  height: 50vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
  position: relative;
  margin-bottom: 0.5em;

  .slider-icon {
    height: 6vh;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: center;
    grid-template-columns: 40% 20% 40%;
    position: absolute;
    z-index: 50;
    opacity: 0.8;
    top: 18vh;

    .icon {
      color: white;
      text-decoration: none;
      font-size: 2.5rem;
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
    top: 25vh;
    z-index: 1000;

    h3 {
      width: 40%;
      height: 100%;
      font-size: 1rem;
      color: white;
      border-top: 1px solid white;
      border-bottom: 1px solid white;
      padding-top: 0.3em;

      &:hover, &:active {
        cursor: pointer;
      }
    }
  }
}

@media only screen and (min-width: 600px) {
  .container {
    height: 60vh;
    margin-top: 0.5em;
    .slider-icon {
      grid-template-columns: 45% 10% 45%;

      .icon {
        font-size: 2.5rem;
      }
    }

    .main-image {
      height: 60vh;
    }

    .slider-button {
      h3 {
        font-size: 1.5rem;
      }
    }
  }
}

@media only screen and (min-width: 1024px) {
  .container {
    height: 65vh;

    .slider-icon {
      grid-template-columns: 45% 10% 45%;

      .icon {
        font-size: 2.5rem;
      }
    }

    .main-image {
      height: 65vh;
    }

    .slider-button {
      top: 27vh;
      h3 {
        font-size: 1.2rem;
      }
    }
  }
}
</style>
