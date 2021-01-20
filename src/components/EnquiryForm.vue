<template>
  <div id="enquiry">
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
};
</script>

<style lang="scss" scoped>
#enquiry {
  width: 90%;
  display: grid;
  justify-items: center;
  align-items: start;
  row-gap: 0.5vh;
}

#form {
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
  margin: 0.5em;
  row-gap: 0.5vh;
  background-attachment: fixed;
  background-repeat: no-repeat;
  background: url(../assets/bio_background.jpg);
  background-size: cover;
  background-position: center;
  padding: 1em 0 2em 0;

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

    &:hover, &:active {
      cursor: pointer;
    }
  }
}

@media only screen and (min-width: 600px) {
  #enquiry {
    width: 90%;
    min-height: 80vh;
    display: grid;
    justify-items: center;
    align-items: start;
    row-gap: 0.5vh;
  }

  #form {
    width: 100%;
    min-height: 80vh;
    display: grid;
    justify-items: center;
    align-items: center;
    margin: 0.5em;
    row-gap: 0.5vh;
    background-attachment: fixed;
    background-repeat: no-repeat;
    background: url(../assets/bio_background_tablet.jpg);
    background-size: cover;
    background-position: center;
    padding: 1em 0 2em 0;

    h3 {
      font-size: 1.5rem;
      padding-top: 2em;
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
    }

    #message-input {
      width: 60%;
      font-size: 1rem;
    }

    .button {
      width: 20%;
      height: 3vh;
      font-size: 1rem;
      margin-top: 0.2em;
      padding-top: 0.2em;
    }
  }
}

@media only screen and (min-width: 1024px) {
  #enquiry {
    width: 32%;
    min-height: 90vh;
    display: grid;
    justify-items: center;
    align-items: start;
    row-gap: 0.5vh;
  }

  #form {
    padding: 1.2em 0 2em 0;

    h3 {
      font-size: 1rem;
      padding: 1em 0 0 0;
      width: 70%;
      margin-top: 1em;
    }

    h4 {
      font-size: 0.8rem;
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
      height: 5vh;
      font-size: 1rem;
      margin-top: 0.2em;
      padding-top: 0.2em;
    }
  }
}
</style>