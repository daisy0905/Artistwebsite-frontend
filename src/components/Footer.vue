<template>
  <div id="footer">
    <div id="container-1">
      <div id="icon-container">
        <img
          @click="getPhone"
          src="../assets/phone-icon.png"
          alt="phone icon"
        />
        <img
          @click="getEmail"
          src="../assets/email-icon.png"
          alt="email icon"
        />
        <img
          @click="getWechat"
          src="../assets/wechat-icon.png"
          alt="weChat icon"
        />
        <img
          @click="getAddress"
          src="../assets/address-icon.png"
          alt="address icon"
        />
      </div>
      <div id="text-container">
        <a v-if="icon == 'phone'" href="tel:13908484972">13908484972</a>
        <a v-if="icon == 'email'" href="mailto:kemin1018@163.com"
          >kemin1018@163.com</a
        >
        <h4 v-if="icon == 'wechat'">TK17Tk17</h4>
        <h4 v-if="icon == 'address'" class="address">
          <span v-if="this.$store.getters.languageGet"
            >中国长沙岳麓区后湖路后湖国际艺术区童柯敏工作室</span
          ><span v-else
            >Studio of Kemin Tong, Houhu International Art Park, Houhu Road,
            Yuelu District, Changsha, China
          </span>
        </h4>
      </div>
    </div>
    <div id="container-2">
      <p @click="goToContact">
        <span v-if="this.$store.getters.languageGet"
          >期待留下您的联系方式 ></span
        ><span v-else>Subscribe To Our Newsletter ></span>
      </p>
    </div>
    <div id="container-3">
      <h4>
        <span v-if="this.$store.getters.languageGet"
          >网页由Daisy Tong制作于2020年</span
        ><span v-else>Created By Daisy Tong @ 2020</span>
      </h4>
      <h4>
        <span v-if="this.$store.getters.languageGet">版权所有</span
        ><span v-else>All Rights Reserved</span>
      </h4>
    </div>
  </div>
</template>

<script>
export default {
  name: "footer-section",
  data() {
    return {
      icon: "phone",
    };
  },
  methods: {
    goToContact: function () {
      this.$router.push("/contact");
    },
    getPhone: function () {
      this.icon = "phone";
    },
    getEmail: function () {
      this.icon = "email";
    },
    getWechat: function () {
      this.icon = "wechat";
    },
    getAddress: function () {
      this.icon = "address";
    },
  },
};
</script>

<style lang="scss" scoped>
#footer {
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
}

#container-1 {
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
  background-color: darkgrey;
}

#icon-container {
  width: 100%;
  height: 7vh;
  display: grid;
  justify-items: center;
  align-items: center;
  grid-template-columns: repeat(4, 1fr);
  padding-top: 1em;

  img {
    width: 30px;
    height: 30px;
    object-fit: cover;

    &:hover,
    &:active {
      width: 35px;
      height: 35px;
      cursor: pointer;
    }
  }
}

#text-container {
  width: 90%;
  height: 7vh;
  display: grid;
  justify-items: center;
  align-items: center;
  padding-top: 1em;

  a {
    font-size: 0.8rem;
    text-decoration: none;
    color: black;
  }

  h4 {
    font-weight: normal;
    font-size: 0.8rem;
    margin: 0;

    &:hover,
    &:active {
      cursor: pointer;
    }
  }
}

#container-2 {
  width: 100%;
  height: 7vh;
  display: grid;
  justify-items: center;
  align-items: start;
  background-color: darkgrey;
  padding-top: 1em;

  p {
    font-weight: bold;
    font-size: 1rem;
    text-align: center;
    color: white;
    text-shadow: 1px 1px 1px black;

    &:hover,
    &:active {
      cursor: pointer;
    }
  }
}

#container-3 {
  width: 100%;
  height: 7vh;
  display: grid;
  grid-template-columns: 1.3fr 1fr;
  justify-items: center;
  align-items: center;
  background-color: black;

  h4 {
    font-size: 0.8rem;
    color: grey;
    font-weight: normal;
  }
}

@media only screen and (min-width: 600px) {
  #icon-container {
    img {
      width: 40px;
      height: 40px;

      &:hover,
      &:active {
        width: 45px;
        height: 45px;
      }
    }
  }

  #text-container {
    a {
      font-size: 1.2rem;
    }

    h4 {
      font-size: 1.2rem;
    }
  }

  #container-2 {
    p {
      font-size: 1.5rem;
    }
  }

  #container-3 {
    h4 {
      font-size: 1rem;
    }
  }
}

@media only screen and (min-width: 1024px) {
  #icon-container {
    img {
      width: 30px;
      height: 30px;

      &:hover,
      &:active {
        width: 40px;
        height: 40px;
      }
    }
  }

  #text-container {
    height: 10vh;
    a {
      font-size: 1.2rem;
    }

    h4 {
      font-size: 1.2rem;
    }
  }

  #container-2 {
    height: 10vh;
    p {
      font-size: 1.2rem;
    }
  }

  #container-3 {
    h4 {
      font-size: 1rem;
    }
  }
}
</style>
