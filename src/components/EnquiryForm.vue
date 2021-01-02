<template>
  <div id="enquiry">
    <div id="form" v-if="display == false">
      <div @click="open" class="close-icon">
        <img src="../assets/close-icon.png" alt="close icon" />
      </div>
      <h4>
        <span v-if="this.$store.getters.languageGet"
          >请留下您的信息，我们将尽快回复，谢谢</span
        ><span v-else>Please leave your message, we will reply ASAP!</span>
      </h4>
      <h4>
        <span v-if="this.$store.getters.languageGet">姓</span
        ><span v-else>Last Name</span>
      </h4>
      <input type="text" class="input" v-model="lastname" />
      <h4>
        <span v-if="this.$store.getters.languageGet">名</span
        ><span v-else>姓</span>
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
      <button @click="postEnquiry">
        <span v-if="this.$store.getters.languageGet">提交</span
        ><span v-else>Submit</span>
      </button>
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
  height: 62vh;
  width: 30%;
  display: grid;
  justify-items: center;
  align-items: start;
  row-gap: 0.5vh;
}

#form {
  width: 90%;
  height: 100vh;
  display: grid;
  justify-items: center;
  align-items: center;
  margin: 0.5em;
  row-gap: 0.5vh;
  background-color: lightgrey;
  padding-bottom: 2em;

  .close-icon {
    width: 100%;
    height: 3vh;
    display: grid;
    justify-items: center;
    align-items: center;
    margin-right: 1em;

    img {
      width: 20px;
      height: 20px;
    }
  }

  h4 {
    width: 90%;
    font-weight: bold;
    font-size: 0.8rem;
    margin: 0.1em;
  }

  p {
    width: 90%;
    font-size: 0.7rem;
    text-align: center;
    margin: 0.1em;
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

  button {
    width: 40%;
    height: 5vh;
    font-size: 0.8rem;
    border: 1px solid black;
    box-shadow: 1px 1px 2px grey;
    font-weight: bold;
    margin-top: 0.5em;
  }
}
</style>