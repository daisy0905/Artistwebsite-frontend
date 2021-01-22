<template>
  <div id="cover-image">
    <div id="preview">
      <div></div>
      <a class="icon" @click="prev" href="#">&#10094;</a>
      <h2>PREVIEW</h2>
      <a class="icon" @click="next" href="#">&#10095;</a>
      <div></div>
    </div>
    <div id="main-image" v-for="i in [currentIndex]" :key="i">
      <img class="color" v-if="mainImageSrc != ''" :src="mainImageSrc" />
      <img
        class="black-and-white"
        v-if="mainImageSrc != ''"
        :src="mainImageSrc"
      />
    </div>
    <div id="image-desktop">
      <div id="color-image" v-for="i in [currentIndex]" :key="i">
        <img class="color" v-if="mainImageSrc != ''" :src="mainImageSrc" />
        <div></div>
      </div>
      <div id="grey-image" v-for="i in [currentIndex]" :key="i">
        <div></div>
        <img class="color" v-if="mainImageSrc != ''" :src="mainImageSrc" />
      </div>
    </div>
    <div class="text-box">
      <h3 class="btn btn-white btn- animate" @click="goToHome">ENTER</h3>
    </div>
  </div>
</template>
<script>
export default {
  name: "Images",
  data() {
    return {
      currentIndex: 0,
      mainImageSrc: "",
    };
  },
  computed: {
    images() {
      if (this.$store.getters.sliderImage == undefined) return;
      console.log(this.$store.getters.sliderImage);
      return this.$store.getters.sliderImage;
    },
  },
  methods: {
    next: function () {
      this.mainImageSrc = this.images[
        Math.abs(this.currentIndex++) % this.images.length
      ].url;
    },
    prev: function () {
      this.mainImageSrc = this.images[
        Math.abs(this.currentIndex--) % this.images.length
      ].url;
    },
    created: function () {
      if (this.images == undefined) return;
      this.mainImageSrc = this.images[
        Math.abs(this.currentIndex) % this.images.length
      ].url;
    },
    goToHome: function () {
      this.$router.push("/home");
    },
  },
  mounted() {
    let interval = setInterval(() => {
      if (this.mainImageSrc != "") {
        clearInterval(interval);
      }
      this.created();
    }, 500);
  },
};
</script>

<style lang="scss" scoped>
#cover-image {
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;

  #preview {
    height: 6vh;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: center;
    grid-template-columns: 25% 10% 30% 10% 25%;
    z-index: 100;
    position: fixed;
    top: -1vh;
    opacity: 0.6;

    .icon {
      color: white;
      text-decoration: none;
      font-size: 2rem;
      text-shadow: 1px 1px 1px black;
    }

    h2 {
      font-weight: bold;
      font-size: 1rem;
      letter-spacing: 5px;
      color: white;
      text-shadow: 1px 1px 1px black;
    }
  }

  #main-image {
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: center;
    grid-template-rows: 1fr 1fr;
    row-gap: 0.5em;

    .color {
      width: 100%;
    }

    .black-and-white {
      width: 100%;
      filter: grayscale(100%);
    }
  }

  #image-desktop {
    display: none;
  }

  .text-box {
    position: fixed;
    bottom: 2vh;
    left: 35vw;
    opacity: 0.6;

    h3 {
      width: 30vw;
      height: 2em;
      padding: 8px 30px;
      border-radius: 0.5em;
      font-size: 1rem;
    }
  }

  .btn:link,
  .btn:visited {
    text-transform: uppercase;
    text-decoration: none;
    display: inline-block;
    transition: all 0.2s;
    position: absolute;
  }

  .btn:hover {
    transform: translateY(-3px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
    cursor: pointer;
  }

  .btn:active {
    transform: translateY(-1px);
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
    cursor: pointer;
  }

  .btn-white {
    background-color: #fff;
    color: #777;
  }

  .btn::after {
    content: "";
    display: inline-block;
    height: 100%;
    width: 100%;
    border-radius: 0.5em;
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
    transition: all 0.4s;
  }

  .btn-white::after {
    background-color: #fff;
  }

  .btn:hover::after {
    transform: scaleX(1.4) scaleY(1.6);
    opacity: 0;
  }

  .btn-animated {
    animation: moveInBottom 5s ease-out;
    animation-fill-mode: backwards;
  }

  @keyframes moveInBottom {
    0% {
      opacity: 0;
      transform: translateY(30px);
    }

    100% {
      opacity: 1;
      transform: translateY(0px);
    }
  }
}

@media only screen and (min-width: 600px) {
  #cover-image {
    height: 100vh;

    #preview {
      height: 10vh;
      top: -2vh;

      .icon {
        font-size: 2.5rem;
        text-shadow: 2px 2px 1px black;
      }

      h2 {
        font-size: 1.8rem;
        letter-spacing: 10px;
        text-shadow: 2px 2px 1px black;
      }
    }

    #image-desktop {
      display: none;
    }

    .text-box {
      h3 {
        padding: 9px 25px;
        font-size: 1.5rem;
      }
    }
  }
}
@media only screen and (min-width: 1024px) {
  #cover-image {
    #preview {
      height: 10vh;
      top: -2vh;
      grid-template-columns: 37% 5% 16% 5% 37%;

      .icon {
        font-size: 2rem;
        text-shadow: 2px 2px 1px black;
      }

      h2 {
        font-size: 1.5rem;
        letter-spacing: 10px;
        text-shadow: 2px 2px 1px black;
      }
    }

    #main-image {
      display: none;
    }

    #image-desktop {
      width: 100%;
      height: 100vh;
      display: grid;
      grid-template-columns: 1fr 1fr;
      justify-items: center;
      align-items: center;

      #color-image {
        width: 100%;
        height: 100%;
        display: grid;
        justify-items: center;
        align-items: start;

        img {
          width: 100%;
        }
      }

      #grey-image {
        width: 100%;
        height: 100%;
        display: grid;
        justify-items: center;
        align-items: end;

        img {
          width: 100%;
          height: auto;
          filter: grayscale(100%);
        }
      }
    }

    .text-box {
      position: fixed;
      bottom: 2vh;
      left: 43vw;
      opacity: 0.8;

      h3 {
        width: 13vw;
        height: 2em;
        padding: 3px 25px;
        font-size: 1.2rem;
      }
    }

    .btn-white {
      background-color: lightgrey;
      border: 3px solid white;
    }
  }
}
</style>