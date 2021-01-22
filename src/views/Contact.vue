<template>
  <div id="contact-page">
    <navigation id="nav"></navigation>
    <nav-desktop id="nav-desktop"></nav-desktop>
    <div id="en-ch">
      <div></div>
      <h4 id="english" @click="showEnglish">EN</h4>
      <h4 id="chinese" @click="showChinese">中文</h4>
      <div></div>
    </div>
    <div id="unit-1">
      <div></div>
      <h2>
        <span v-if="this.$store.getters.languageGet">期待与您联系！</span
        ><span v-else>I'D LOVE TO HEAR FROM YOU</span>
      </h2>
      <div></div>
    </div>
    <div id="container">
      <div class="contact-mobile">
        <div class="item">
          <img src="../assets/phone-icon.png" alt="phone icon" />
          <a href="tel:13908484972">13908484972</a>
        </div>
        <div class="item">
          <img src="../assets/email-icon.png" alt="email icon" />
          <a href="mailto:kemin1018@163.com">kemin1018@163.com</a>
        </div>
        <div class="item">
          <img src="../assets/wechat-icon.png" alt="weChat icon" />
          <h3>TK17Tk17</h3>
        </div>
        <div class="item">
          <img src="../assets/address-icon.png" alt="address icon" />
          <h3>
            <span v-if="this.$store.getters.languageGet"
              >中国长沙岳麓区后湖路后湖国际艺术区童柯敏工作室</span
            ><span v-else
              >Studio of Kemin Tong, Houhu International Art Park, Houhu Road,
              Yuelu District, Changsha, China</span
            >
          </h3>
        </div>
      </div>
      <div class="contact-tablet">
        <div class="item-tablet">
          <div class="item">
            <img src="../assets/phone-icon.png" alt="phone icon" />
            <a href="tel:13908484972">13908484972</a>
          </div>
          <div class="item">
            <img src="../assets/email-icon.png" alt="email icon" />
            <a href="mailto:kemin1018@163.com">kemin1018@163.com</a>
          </div>
          <div class="item">
            <img src="../assets/wechat-icon.png" alt="weChat icon" />
            <h3>TK17Tk17</h3>
          </div>
        </div>
        <div class="item">
          <img src="../assets/address-icon.png" alt="address icon" />
          <h3>
            <span v-if="this.$store.getters.languageGet"
              >中国长沙岳麓区后湖路后湖国际艺术区童柯敏工作室</span
            ><span v-else
              >Studio of Kemin Tong, Houhu International Art Park, Houhu Road,
              Yuelu District, Changsha, China</span
            >
          </h3>
        </div>
      </div>
      <div id="desktop">
        <div class="form">
          <h3>
            <span v-if="this.$store.getters.languageGet">保持联络！</span
            ><span v-else>STAY IN TOUCH!</span>
          </h3>
          <div class="contact-form">
            <div class="box">
              <p>
                <span v-if="this.$store.getters.languageGet">姓</span
                ><span v-else>Last Name</span>
              </p>
              <input type="text" class="input" v-model="lastname" />
            </div>
            <div class="box">
              <p>
                <span v-if="this.$store.getters.languageGet">名</span
                ><span v-else>First Name</span>
              </p>
              <input type="text" class="input" v-model="firstname" />
            </div>
            <div class="box">
              <p>
                <span v-if="this.$store.getters.languageGet">电话</span
                ><span v-else>Phone Number</span>
              </p>
              <input type="text" class="input" v-model="phone" />
            </div>
            <div class="box">
              <p>
                <span v-if="this.$store.getters.languageGet">邮箱</span
                ><span v-else>Email</span>
              </p>
              <input type="text" class="input" v-model="email" />
            </div>
            <div class="box">
              <p>
                <span v-if="this.$store.getters.languageGet">微信</span
                ><span v-else>WeChat ID</span>
              </p>
              <input type="text" class="input" v-model="wechat" />
            </div>
            <h4 class="button" @click="createContact">
              <span v-if="this.$store.getters.languageGet">提交</span
              ><span v-else>Submit</span>
            </h4>
            <p>{{ submitStatus }}</p>
          </div>
        </div>
        <div class="unit-2">
          <h3>
            <span v-if="this.$store.getters.languageGet">童柯敏工作室</span
            ><span v-else>TONG'S ART STUDIO</span>
          </h3>
          <img src="../assets/studio.jpg" alt="the image of studio" />
        </div>
      </div>
    </div>
    <footer-contact></footer-contact>
  </div>
</template>

<script>
import Navigation from "../components/Nav.vue";
import NavDesktop from "../components/NavDesktop.vue";
import axios from "axios";
import FooterContact from "../components/FooterContact.vue";
import cookies from "vue-cookies";
export default {
  components: {
    Navigation,
    NavDesktop,
    FooterContact,
  },
  data() {
    return {
      firstname: "",
      lastname: "",
      phone: "",
      email: "",
      wechat: "",
      submitStatus: "",
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
    createContact: function () {
      axios
        .request({
          url: "https://artisttongkemin.ml/api/visitor",
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          data: {
            firstname: this.firstname,
            lastname: this.lastname,
            phone_number: this.phone,
            email: this.email,
            wechat: this.wechat,
          },
        })
        .then((response) => {
          console.log(response);
          this.submitStatus =
            "your contact information has been successfully submitted!";
        })
        .catch((error) => {
          console.log(error);
          this.submitStatus = "Falied to submit!";
        });
    },
  },
  mounted() {
    this.showEnglish();
  },
};
</script>

<style lang="scss" scoped>
#contact-page {
  width: 100%;
  display: grid;
  align-items: start;
  justify-items: center;
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
  }
}

#unit-1 {
  width: 100%;
  height: 25vh;
  background-attachment: fixed;
  background-repeat: no-repeat;
  background: url(../assets/studio-3.jpg);
  background-size: cover;
  background-position: top;
  display: grid;
  align-items: center;
  justify-content: center;
  grid-template-columns: 15% 70% 15%;
  margin-top: 0.5em;

  h2 {
    font-weight: bold;
    font-size: 1.5rem;
    margin: 0;
    text-align: center;
    text-shadow: 2px 2px 1px white;
    letter-spacing: 0.2em;
  }
}

#container {
  min-height: 100vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: start;
  background-attachment: fixed;
  background-repeat: no-repeat;
  background: url(../assets/bio_background_mobile.jpg);
  background-size: cover;
  background-position: center;
}

.contact-mobile {
  min-height: 30vh;
  width: 80%;
  display: grid;
  justify-items: center;
  align-items: center;
  margin-top: 1em;
  row-gap: 1vh;

  .item {
    height: 10vh;
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: center;

    img {
      width: 30px;
      height: 30px;
      object-fit: cover;
    }

    a {
      font-size: 1rem;
      text-decoration: none;
      color: black;
      font-weight: bold;

      &:hover,
      &:active {
        cursor: pointer;
      }
    }

    h3 {
      font-weight: bold;
      font-size: 1rem;
      margin: 0.5em;
    }
  }
}

.contact-tablet {
  display: none;
}

#desktop {
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
  margin-top: 1em;
}

.form {
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;

  h3 {
    width: 40%;
    font-weight: bold;
    font-size: 1rem;
    margin-top: 2em;
    border-bottom: 1px solid black;
  }

  .contact-form {
    width: 80%;
    display: grid;
    justify-items: center;
    align-items: center;
    row-gap: 0.8vh;
    margin: 2em 0 1em 0;
    padding: 1em 0 1em 0;
    box-shadow: 3px 3px 3px #657786;
    border: 1px solid black;

    .box {
      width: 100%;
      height: 5vh;
      display: grid;
      justify-items: center;
      align-items: center;
      grid-template-columns: 40% 60%;

      p {
        width: 90%;
        font-size: 0.8rem;
        text-align: left;
        margin-left: 3em;
        font-weight: bold;
      }

      .input {
        width: 60%;
        height: 3vh;
        border: 1px solid #aab8c2;
        text-align: center;
        background-color: transparent;
        border: 1px solid black;
      }
    }

    .button {
      width: 25vw;
      height: 3vh;
      font-size: 0.8rem;
      border: 1px solid black;
      box-shadow: 1px 1px 2px grey;
      font-weight: bold;
      margin-top: 1em;
    }

    p {
      width: 70%;
      height: 2em;
      font-size: 0.8rem;
      margin-top: 1em;
    }
  }
}

.unit-2 {
  min-height: 50vh;
  width: 80%;
  display: grid;
  justify-items: center;
  align-items: center;
  margin-top: 1em;

  h3 {
    width: 65%;
    font-weight: bold;
    font-size: 1rem;
    margin: 2em 0 2em 0;
    border-bottom: 1px solid black;
  }

  img {
    width: 100%;
    margin-bottom: 1em;
    box-shadow: 3px 3px 3px #657786;
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
  #unit-1 {
    height: 30vh;
    margin-top: 0.8em;

    h2 {
      font-size: 2rem;
    }
  }

  .contact-mobile {
    display: none;
  }

  .contact-tablet {
    min-height: 20vh;
    width: 80%;
    display: grid;
    justify-items: center;
    align-items: center;
    margin-top: 1em;

    .item-tablet {
      width: 100%;
      height: 15vh;
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      justify-items: center;
      align-items: center;
      margin-top: 1em;

      .item {
        img {
          width: 40px;
          height: 40px;
        }

        a {
          font-size: 1.5rem;
          text-decoration: none;
          color: black;
          font-weight:bold;
          display:block;

          &:hover,
          &:active {
            cursor: pointer;
          }
        }

        h3 {
          font-size: 1.5rem;
        }
      }
    }

    .item {
      img {
        width: 40px;
        height: 40px;
        margin-bottom: 1em;
      }

      h3 {
        font-size: 1.5rem;
      }
    }
  }

  .form {
    h3 {
      width: 35%;
      font-size: 1.5rem;
    }

    .contact-form {
      width: 60%;

      .box {
        p {
          font-size: 1.2rem;
        }
      }

      .button {
        width: 20vw;
        font-size: 1.2rem;
      }

      p {
        width: 70%;
        height: 2em;
        font-size: 1rem;
      }
    }
  }

  .unit-2 {
    width: 60%;
    display: grid;
    justify-items: center;
    align-items: center;
    margin-top: 1em;

    h3 {
      font-size: 1.5rem;
      margin-bottom: 1em;
    }

    img {
      width: 100%;
      height: 40vh;
      object-fit: cover;
      margin-bottom: 2em;
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

  #unit-1 {
    height: 60vh;

    h2 {
      font-size: 2rem;
    }
  }

  .contact-tablet {
    min-height: 40vh;

    .item-tablet {
      width: 100%;
      height: 15vh;

      .item {
        img {
          width: 40px;
          height: 40px;
        }

        a {
          font-size: 1.2rem;
        }

        h3 {
          font-size: 1.2rem;
        }
      }
    }

    .item {
      img {
        width: 40px;
        height: 40px;
      }

      h4 {
        font-size: 1rem;
      }
    }
  }

  #desktop {
    width: 80%;
    height: 60vh;
    grid-template-columns: 1fr 1fr;
    margin-bottom: 2em;
  }

  .form {
    h3 {
      width: 60%;
      font-size: 1.2rem;
    }

    .contact-form {
      height: 45vh;
      .box {
        p {
          font-size: 1rem;
        }
      }

      .button {
        width: 8vw;
        height: 5vh;
        font-size: 1.2rem;
      }

      p {
        width: 70%;
        height: 2em;
        font-size: 0.8rem;
        margin-top: 1em;
      }
    }
  }
  .unit-2 {
    width: 60%;

    h3 {
      width: 100%;
      font-weight: bold;
      font-size: 1.2rem;
      margin: 1em 0 2em 0;
    }

    img {
      width: 100%;
      height: 45vh;
      object-fit: cover;
      margin-bottom: 1em;
    }
  }
}
</style>