<template>
  <div id="artwork-list">
    <div id="header">
      <div class="icon">
        <img
          @click="backToArtwork"
          src="../assets/left-arrow-icon.png"
          alt="nav icon"
        />
      </div>
      <h3>KEMIN TONG</h3>
      <div></div>
    </div>
    <div id="artwork-container-1" v-if="this.searchArtworks.length == 0">
      <h2>No Artwork Matches Your Search, Please Try Again!</h2>
      <h2>没有检索到相关画作，请重试！</h2>
    </div>
    <div v-else id="artwork-container-2">
      <searched-artword-card
        class="artworks"
        v-for="art in searchArtworks"
        :key="art.id"
        :art="art"
      ></searched-artword-card>
    </div>
    <footer-section id="footer"></footer-section>
    <div id="go-to-top">
      <a href="#artwork-list">TO TOP</a>
    </div>
  </div>
</template>

<script>
import cookies from "vue-cookies";
import axios from "axios";
import SearchedArtwordCard from "../components/SearchedArtwordCard.vue";
import FooterSection from "../components/Footer.vue";

export default {
  components: {
    SearchedArtwordCard,
    FooterSection,
  },
  data() {
    return {
      searchArtworks: [],
      content: cookies.get("artContent"),
    };
  },
  methods: {
    getSearchArtworks: function () {
      axios
        .request({
          url: "https://artisttongkemin.ml/api/artwork",
          method: "GET",
          headers: {
            "Content-Type": "application/json",
          },
          params: {
            content: this.content,
          },
        })
        .then((response) => {
          console.log(response);
          this.searchArtworks = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    backToArtwork: function () {
      this.$router.push("/artwork");
    },
  },
  mounted() {
    this.getSearchArtworks();
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
  row-gap: 0.5vh;
}

#header {
  height: 3em;
  width: 100%;
  display: grid;
  grid-template-columns: 10% 80% 10%;
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
      height: 20px;
      object-fit: cover;

      &:hover, &:active {
        cursor: pointer;
      }
    }
  }

  h3 {
    font-weight: bold;
    font-size: 1rem;
    letter-spacing: 5px;
  }
}

#artwork-container-1 {
  width: 100%;
  min-height: 70vh;
  display: grid;
  justify-items: center;
  align-items: start;
  align-content: start;
  background-attachment: fixed;
  background-repeat: no-repeat;
  background: url(../assets/bio_background_mobile.jpg);
  background-size: cover;
  background-position: center;
  padding-top: 5em;

  h2 {
    width: 70%;
    font-weight: bold;
    font-size: 1.5rem;
    margin: 1em 0 1em 0;
  }
}

#artwork-container-2 {
  width: 100%;
  min-height: 100vh;
  display: grid;
  justify-items: center;
  align-items: start;
  align-content: start;
  row-gap: 1em;
  margin-bottom: 2em;

  .artworks {
    height: 100%;
    display: grid;
    justify-items: center;
    align-items: start;
    align-content: start;
  }
}

#go-to-top {
  position: fixed;
  bottom: 30vh;
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
    padding: 0.5em;
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

#id {
  position: fixed;
  bottom: 0;
}
@media only screen and (min-width: 600px) {
  #header {
    height: 4.5em;
    .icon {
      img {
        height: 30px;
        object-fit: cover;
      }
    }

    h3 {
      font-size: 1.5rem;
    }
  }

  .artworks {
    min-height: 60vh;
  }

  #go-to-top {
    right: 0;
    width: 5vw;
    height: 10vh;

    a {
      font-size: 0.8rem;
    }
  }
}

@media only screen and (min-width: 1024px) {
  #artwork-container-2 {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }

  #go-to-top {
    bottom: 35vh;
    width: 5vw;
    height: 10vh;

    a {
      font-size: 0.8rem;
    }
  }
}
</style>