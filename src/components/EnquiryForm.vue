<template>
  <div id="enquiry">
    <div id="image-container">
      <img :src="url" />
    </div>
    <div id="form" v-if="display == false">
      <h3>
        <span v-if="this.$store.getters.languageGet"
          >请留下您的信息，我们将尽快回复，谢谢!</span
        ><span v-else>Please leave your message, we will reply ASAP!</span>
      </h3>
      <h4>
        <span v-if="this.$store.getters.languageGet">姓</span
        ><span v-else>Last Name</span>
      </h4>
      <input type="text" class="input" v-model="lastname" />
      <h4>
        <span v-if="this.$store.getters.languageGet">名</span
        ><span v-else>First Name</span>
      </h4>
      <input type="text" class="input" v-model="firstname" />
      <h4>
        <span v-if="this.$store.getters.languageGet">邮箱</span
        ><span v-else>Email</span>
      </h4>
      <input type="text" class="input" v-model="email" />
      <h4>
        <span v-if="this.$store.getters.languageGet">电话</span
        ><span v-else>Phone Number</span>
      </h4>
      <input type="text" class="input" v-model="phone_number" />
      <h4>
        <span v-if="this.$store.getters.languageGet">留言</span
        ><span v-else>Message</span>
      </h4>
      <textarea id="message-input" v-model="message"></textarea>
      <h4 class="button" @click="postEnquiry">
        <span v-if="this.$store.getters.languageGet">提交</span
        ><span v-else>Submit</span>
      </h4>
      <p>{{ enquiryStatus }}</p>
    </div>
  </div>
</template>

<script>
import cookies from "vue-cookies";
import axios from "axios";

export default {
  data() {
    return {
      firstname: "",
      lastname: "",
      email: "",
      phone_number: "",
      message: "",
      enquiryStatus: "",
      review: 0,
      display: false,
    };
  },
  methods: {
    postEnquiry: function () {
      axios
        .request({
          url: "https://artisttongkemin.ml/api/enquiry",
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          data: {
            art_id: cookies.get("id"),
            firstname: this.firstname,
            lastname: this.lastname,
            email: this.email,
            phone_number: this.phone_number,
            message: this.message,
            review: this.review,
          },
        })
        .then((response) => {
          console.log(response);
          this.enquiryStatus = "Your enquiry has been submitted!";
          setTimeout(() => {
            this.$router.push("/artwork");
          }, 1000);
        })
        .catch((error) => {
          console.log(error);
          this.enquiryStatus = "Failed to submit!";
        });
    },
    open: function () {
      this.display = !this.display;
    },
  },
  computed: {
    url() {
      if (this.$store.state.artwork[0] == undefined) return "";
      console.log(this.$store.state.artwork[0].url);
      return this.$store.state.artwork[0].url;
    },
  },
  mounted() {
    if (this.$store.state.artwork.length == 0) {
      this.$store.dispatch("getArtwork");
    }
  },
};
</script>

<style lang="scss" scoped>
#enquiry {
  width: 90%;
  display: grid;
  justify-items: center;
  align-items: start;
  row-gap: 0.5vh;
  position: relative;
}

#image-container {
  width: 100%;
  min-height: 70vh;
  display: grid;
  justify-items: center;
  align-items: center;
  margin-bottom: 1em;
  box-shadow: 4px 4px 3px grey;

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    filter: grayscale(100%);
  }
}

#form {
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
  margin: 0.5em;
  row-gap: 0.5vh;
  padding: 1em 0 2em 0;
  position: absolute;
  top: 0;

  h3 {
    width: 90%;
    font-weight: bold;
    font-size: 1rem;
    color: white;
    padding-top: 0.8em;
  }

  h4 {
    width: 90%;
    font-weight: bold;
    font-size: 0.8rem;
    margin: 0.1em;
    color: white;
  }

  p {
    width: 90%;
    font-size: 0.7rem;
    text-align: center;
    margin: 0.1em;
    color: white;
  }

  .input {
    width: 70%;
    height: 3vh;
    border: 1px solid #aab8c2;
    text-align: center;
    margin: 0.1em;
  }

  #message-input {
    width: 70%;
    height: 15vh;
    border: 1px solid #aab8c2;
    text-align: center;
    font-size: 0.8rem;
  }

  .button {
    width: 40%;
    height: 5vh;
    font-size: 0.8rem;
    border: 1px solid black;
    box-shadow: 1px 1px 2px grey;
    font-weight: bold;
    margin-top: 0.5em;
    background-color: white;
    color: black;
    padding-top: 0.5em;

    &:hover,
    &:active {
      cursor: pointer;
    }
  }
}

@media only screen and (min-width: 600px) {
  #enquiry {
    min-height: 75vh;
  }

  #image-container {
    width: 90%;
    box-shadow: 6px 6px 3px grey;
    margin-bottom: 0;

  }

  #form {
    padding: 0 0 2em 0;

    h3 {
      font-size: 1.5rem;
      padding: 1em 0 1em 0;
    }

    h4 {
      font-size: 1.2rem;
    }

    p {
      font-size: 1rem;
      padding-bottom: 1em;
    }

    .input {
      width: 60%;
      height: 4vh;
    }

    #message-input {
      width: 60%;
      font-size: 1rem;
    }

    .button {
      width: 20%;
      height: 3vh;
      font-size: 1rem;
      margin-top: 1em;
      padding-top: 0.2em;
    }
  }
}

@media only screen and (min-width: 1024px) {
  #enquiry {
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: start;
    row-gap: 0.5vh;
    border: 3px solid white;
    background-attachment: fixed;
    background-repeat: no-repeat;
    background: url(../assets/artwork_background.jpg);
    background-size: cover;
    background-position: center;
  }

  #image-container {
    width: 35%;
    margin-bottom: 1em;
    height: 90vh;
    margin-top: 1em;
  }

  #form {
    width: 35%;
    padding: 0 0 2em 0;
    margin: 0;

    h3 {
      font-size: 1.2rem;
      padding: 1em 0 0 0;
      margin-top: 1em;
    }

    h4 {
      font-size: 1rem;
      margin: 0.2em;
    }

    p {
      font-size: 1rem;
      padding-bottom: 1em;
    }

    .input {
      width: 60%;
    }

    #message-input {
      width: 60%;
      font-size: 1rem;
    }

    .button {
      width: 20%;
      height: 6vh;
      font-size: 1rem;
      margin-top: 0.2em;
      padding-top: 0.2em;
    }
  }
}
</style>