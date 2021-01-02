<template>
  <div id="image-upload">
    <img
      v-if="loading"
      src="../assets/loading.gif"
      alt="loading preview icon"
    />
    <input
      v-else
      type="file"
      accept="image/*"
      @change="onchange"
      id="file-input"
    />
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      name: "",
      url: "",
      loading: false,
    };
  },
  methods: {
    onchange(e) {
      this.loading = true;
      const file = e.target.files[0];
      this.name = file.name;
      let formData = new FormData();
      formData.set("file", file, this.name);
      axios
        .post("https://artisttongkemin.ml/api/upload", formData, {
          headers: {
            "content-type": "multipart/form-data",
          },
        })
        .then((response) => {
          console.log(response);
          this.url = "https://artisttongkemin.ml/img/uploadimage/" + this.name;
          this.$emit("newImage", this.url);
          this.loading = false;
        });
    },
  },
};
</script>

<style lang="scss" scoped>
#image-upload {
  font-size: 0.8rem;
  width: 80%;
  display: grid;
  justify-items: center;
  align-items: center;

  #file-input {
    width: 100%;
    border: None;
    background-color: white;
  }

  img {
    width: 200px;
  }
}

@media only screen and (min-width: 600px) {
  #image-upload {
    width: 80%;

    #file-input {
      font-size: 1rem;
      margin: 0 0 1em 3.5em;
    }

    img {
      width: 250px;
    }
  }
}

@media only screen and (min-width: 1024px) {
  #image-upload {
    width: 80%;

    #file-input {
      font-size: 1rem;
      margin: 0 0 1em 3em;
    }

    img {
      width: 250px;
    }
  }
}
</style>
