<template>
  <div id="artwork">
    <navigation id="nav"></navigation>
    <nav-desktop id="nav-desktop"></nav-desktop>
    <div id="en-ch">
      <div></div>
      <h4 id="english" @click="showEnglish">EN</h4>
      <h4 id="chinese" @click="showChinese">中文</h4>
      <div></div>
    </div>
    <div id="search-bar">
      <div></div>
      <input type="text" class="search" v-model="content" />
      <img
        @click="getArtworkList"
        src="https://cdn2.iconfinder.com/data/icons/font-awesome/1792/search-512.png"
        alt="search icon"
      />
      <div></div>
    </div>
    <div id="content-container">
      <div id="image-container">
        <img :src="url" />
      </div>
      <div id="text-container">
        <div id="description">
          <h3>{{ name }}</h3>
          <p>{{ length }} X {{ width }}</p>
          <p>{{ material }}</p>
          <p>{{ completed_at }}</p>
        </div>
        <div id="button">
          <p @click="statusCheck">{{ status }}</p>
          <p @click="showEnquiryForm" class="btn-1">
            <span v-if="this.$store.getters.languageGet">询价</span
            ><span v-else>Enquiry</span>
          </p>
          <p class="btn-1" v-if="artStatus == true" @click="addToCart">
            <span v-if="this.$store.getters.languageGet">下订单</span
            ><span v-else>Add to Cart</span>
          </p>
          <p v-else class="btn-2">
            <span v-if="this.$store.getters.languageGet">下订单</span
            ><span v-else>Add to Cart</span>
          </p>
          <div id="alert" v-if="show == true">
            <button class="closebtn" @click="close">&times;</button>
            <h4>{{ updateStatus }}</h4>
          </div>
        </div>
      </div>
    </div>
    <enquiry-form class="enquiry-form" v-if="open"></enquiry-form>
    <footer-section></footer-section>
  </div>
</template>

<script>
import Navigation from "../components/Nav.vue";
import NavDesktop from "../components/NavDesktop.vue";
import cookies from "vue-cookies";
import axios from "axios";
import EnquiryForm from "../components/EnquiryForm.vue";
import FooterSection from "../components/Footer.vue";
export default {
  components: {
    Navigation,
    NavDesktop,
    EnquiryForm,
    FooterSection,
  },
  data() {
    return {
      content: "",
      artStatus: true,
      updateStatus: "",
      show: false,
      open: false,
    };
  },
  methods: {
    statusCheck: function () {
      console.log(this.$store.state.artwork[0].status);
      if (this.$store.state.artwork[0].status == undefined) return;
      if (this.$store.state.artwork[0].status == "Available") {
        this.artStatus = true;
      } else if (this.$store.state.artwork[0].status == "On hold") {
        this.artStatus = false;
      } else if (this.$store.state.artwork[0].status == "Sold") {
        this.artStatus = false;
      }
    },
    addToCart: function () {
      this.show = true;
      if (this.artStatus == true) {
        return this.changeStatus();
      }
    },
    changeStatus: function () {
      axios
        .request({
          url: "https://artisttongkemin.ml/api/artwork",
          method: "PATCH",
          headers: {
            "Content-Type": "application/json",
          },
          data: {
            id: cookies.get("id"),
            status: "On hold",
          },
        })
        .then((response) => {
          console.log(response);
          this.artStatus = false;
          this.updateStatus = "Success to add!";
          this.$store.dispatch("getArtwork");
        })
        .catch((error) => {
          console.log(error);
          this.updateStatus = "Failed to add!";
        });
    },
    close: function () {
      document.getElementById("alert").style.display = "none";
    },
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
    getArtworkList: function () {
      cookies.set("artContent", this.content);
      this.$router.push("/artworklist");
    },
    showEnquiryForm: function () {
      this.open = !this.open;
    },
    closeDesktop: function () {
      document.getElementById("alert-desktop").style.display = "none";
    }
  },
  mounted: function () {
    if (this.$store.state.artwork.length == 0) {
      this.$store.dispatch("getArtwork");
    }
    setTimeout(() => {
      this.statusCheck();
    }, 500),
    this.showEnglish();
  },
  computed: {
    name() {
      if (this.$store.state.artwork[0] == undefined) return "";
      return this.$store.state.artwork[0].name;
    },
    length() {
      if (this.$store.state.artwork[0] == undefined) return "";
      return this.$store.state.artwork[0].length;
    },
    width() {
      if (this.$store.state.artwork[0] == undefined) return "";
      return this.$store.state.artwork[0].width;
    },
    completed_at() {
      if (this.$store.state.artwork[0] == undefined) return "";
      return this.$store.state.artwork[0].completed_at;
    },
    url() {
      if (this.$store.state.artwork[0] == undefined) return "";
      return this.$store.state.artwork[0].url;
    },
    material() {
      if (this.$store.state.artwork[0] == undefined) return "";
      return this.$store.state.artwork[0].material;
    },
    status() {
      if (this.$store.state.artwork[0] == undefined) return "";
      return this.$store.state.artwork[0].status;
    },
  },
};
</script>

<style lang="scss" scoped>
#artwork {
  min-height: 100vh;
  width: 100%;
  display: grid;
  align-items: start;
  justify-items: center;
  position: relative;
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
    margin: 0;

    &:hover,
    &:active {
      cursor: pointer;
    }
  }
}

#search-bar {
  min-height: 8vh;
  width: 100%;
  display: grid;
  align-items: center;
  justify-items: center;
  grid-template-columns: 25% 40% 15% 20%;

  .search {
    height: 3vh;
    width: 100%;
    background-color: white;
    text-align: center;
    color: grey;
    font-size: 0.8rem;
  }

  img {
    width: 25px;
  }
}

#content-container {
  width: 100%;
  display: grid;
  align-items: start;
  justify-items: center;

  #image-container {
    min-height: 20vh;
    width: 100%;
    display: grid;
    align-items: start;
    justify-items: center;

    img {
      width: 90%;
      height: auto;
      vertical-align: super;
      border: 4px solid darkgrey;
    }
  }

  #text-container {
    width: 100%;
    display: grid;
    align-items: start;
    justify-items: center;
    margin-top: 1em;

    #description {
      min-height: 20vh;
      width: 100%;
      display: grid;
      align-items: center;
      justify-items: center;
      margin: 0;

      h3 {
        width: 90%;
        font-weight: bold;
        font-size: 1rem;
        text-align: center;
        margin: 0;
        letter-spacing: 1px;
        margin-top: 0.5em;
      }

      p {
        font-size: 1rem;
        margin: 0;
      }
    }

    #button {
      min-height: 30vh;
      width: 40%;
      display: grid;
      align-items: center;
      justify-items: center;

      p {
        width: 100%;
        background-color: grey;
        font-size: 1rem;
        margin: 0;
        padding: 0.5em;
        color: white;
        font-weight: bold;
        letter-spacing: 3px;
      }

      .btn-1 {
        width: 100%;
        height: 5vh;
        font-size: 1rem;
        border: 1px solid black;
        box-shadow: 1px 1px 2px grey;
        font-weight: bold;
        padding-top: 0.5em;
        background-color: white;
        color: black;

        &:hover,
        &:active {
          cursor: pointer;
        }
      }

      .btn-2 {
        width: 100%;
        height: 5vh;
        font-size: 1rem;
        border: 1px solid black;
        box-shadow: 1px 1px 2px grey;
        font-weight: bold;
        text-decoration: line-through;
        padding-top: 0.5em;
        background-color: white;
        color: black;
      }

      #alert {
        height: 5vh;
        width: 40vw;
        background-color: lightgrey;

        .closebtn {
          height: 100%;
          margin-left: 15px;
          color: black;
          font-weight: bold;
          float: right;
          font-size: 22px;
          line-height: 20px;
          cursor: pointer;
          transition: 0.3s;
          text-align: center;

          :hover {
            color: black;
          }
        }

        h4 {
          font-size: 0.8rem;
          text-align: center;
          margin: 0;
        }
      }
    }
  }
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

  #search-bar {
    .search {
      height: 4vh;
      font-size: 1.2rem;
    }

    img {
      width: 30px;
    }
  }

  #content-container {
    #image-container {
      img {
        border: 6px solid darkgrey;
      }
    }

    #text-container {
      #description {
        h3 {
          font-size: 1.5rem;
        }

        p {
          font-size: 1.5rem;
        }
      }

      #button {
        width: 35%;

        p {
          font-size: 1.5rem;
        }

        .btn-1 {
          font-size: 1.5rem;
        }

        .btn-2 {
          font-size: 1.5rem;
        }

        #alert {
          height: 5vh;
          width: 40vw;
          background-color: lightgrey;

          .closebtn {
            font-size: 25px;
            line-height: 20px;
          }

          h4 {
            font-size: 1.2rem;
          }
        }
      }
    }
  }
}

@media only screen and (min-width: 1024px) {
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

  #search-bar {
    height: 10vh;
    grid-template-columns: 3% 30% 10% 57%;
    margin: 0 1em 1em 1em;

    .search {
      height: 6vh;
    }
  }

  #content-container {
    min-height: 40vh;
    grid-template-columns: 1.5fr 1fr;
    margin-bottom: 2em;
    position: relative;

    #image-container {
      height: 100%;
    }

    #text-container {
      height: 100%;
      margin-top: 0;
      
      #description {
        // margin-bottom: 2em;
        h3 {
          font-size: 1.2rem;
        }

        p {
          font-size: 1.2rem;
          margin-top: 1em;
        }
      }

      #button {
        width: 15%;
        min-height: 50vh;
        position: absolute;
        bottom: 0;
        right: 13vw;

        p {
          font-size: 1.2rem;
          margin-top: 2em;
        }

        .btn-1 {
          font-size: 1.2rem;
          height: 2.5em;
        }

        .btn-2 {
          font-size: 1.2rem;
          height: 2.5em;
        }

        #alert {
          height: 7vh;
          width: 100%;
          margin-top: 1em;


          h4 {
            font-size: 1rem;
            padding-top: 0.3em;
          }
        }
      }
    }
  }
}
</style>