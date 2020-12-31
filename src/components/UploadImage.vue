<template>
  <div id="image-upload">
    <img v-if="loading" src="" alt="" />
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
    width: 100%;
    display: grid;
    justify-items: center;
    align-items: center;

    #file-input {
        width: 100%;
        border: None;
    }
    // img {
    //     width: 100px;
    // }
}  
</style>
