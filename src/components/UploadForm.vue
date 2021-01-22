<template>
  <div>
    <div id="upload-form">
      <h3>
        <span v-if="this.$store.getters.languageGet">名称</span
        ><span v-else>Name</span>
      </h3>
      <input type="text" id="name-input" class="input" v-model="name" />
      <h3>
        <span v-if="this.$store.getters.languageGet">长</span
        ><span v-else>Length</span>
      </h3>
      <input type="text" id="length-input" class="input" v-model="length" />
      <h3>
        <span v-if="this.$store.getters.languageGet">宽</span
        ><span v-else>Width</span>
      </h3>
      <input type="text" id="width-input" class="input" v-model="width" />
      <h3>
        <span v-if="this.$store.getters.languageGet">完成年份</span
        ><span v-else>Completed at</span>
      </h3>
      <input
        type="text"
        id="completed-input"
        class="input"
        v-model="completed_at"
      />
      <h3>
        <span v-if="this.$store.getters.languageGet">材料</span
        ><span v-else>Material</span>
      </h3>
      <input type="text" id="material-input" class="input" v-model="material" />
      <h3>
        <span v-if="this.$store.getters.languageGet">分类</span
        ><span v-else>Category</span>
      </h3>
      <input type="text" id="category-input" class="input" v-model="category" />
      <h3>
        <span v-if="this.$store.getters.languageGet">状态</span
        ><span v-else>Status</span>
      </h3>
      <input type="text" id="status-input" class="input" v-model="status" />
      <h3>
        <span v-if="this.$store.getters.languageGet">作品链接</span
        ><span v-else>Image URL</span>
      </h3>
      <input type="text" id="url-input" class="input" v-model="url" />
    </div>
    <upload-image class="upload-image" @newImage="newImage"></upload-image>
    <div v-if="this.url != ''" class="preview">
      <img :src="url" alt="" />
    </div>
    <div class="submit-btn">
      <div></div>
      <button @click="uploadArtwork">
        <span v-if="this.$store.getters.languageGet">上传</span
        ><span v-else>Upload</span>
      </button>
      <div></div>
    </div>
    <h3>{{ uploadStatus }}</h3>
  </div>
</template>

<script>
import axios from "axios";
import UploadImage from "./UploadImage.vue";
export default {
  components: {
    UploadImage,
  },
  data() {
    return {
      name: "",
      length: "",
      width: "",
      completed_at: "",
      material: "",
      category: "",
      status: "",
      url: "",
      uploadStatus: "",
      display: false,
    };
  },
  methods: {
    uploadArtwork: function () {
      axios
        .request({
          url: "https://artisttongkemin.ml/api/artwork",
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          data: {
            name: this.name,
            length: this.length,
            width: this.width,
            completed_at: this.completed_at,
            material: this.material,
            category: this.category,
            status: this.status,
            url: this.url,
          },
        })
        .then((response) => {
          console.log(response);
          this.uploadStatus = "Success";
        })
        .catch((error) => {
          console.log(error);
          this.uploadStatus = "Error";
        });
    },
    newImage: function (data) {
      this.url = data;
    },
  },
};
</script>

<style lang="scss" scoped>
#upload-form {
  min-height: 50vh;
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  justify-items: left;
  align-items: left;
  margin-top: 5em;

  h3 {
    font-weight: bold;
    font-size: 1rem;
    text-align: left;
    letter-spacing: 2px;
    margin-left: 2em;
  }

  .input {
    width: 80%;
    height: 4vh;
    background-color: white;
    border: 1px solid #aab8c2;
    margin: 0 0 1em 0;
    border-bottom: 2px solid darkgrey;
    text-align: center;
    font-size: 0.8rem;
  }
}

.upload-image {
  width: 100%;
  margin-left: 2em;
}

.preview {
  width: 100%;
  min-height: 20vh;
  display: grid;
  justify-items: center;
  align-items: center;
  margin-top: 1em;

  img {
    height: 150px;
  }
}

.submit-btn {
  height: 15vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
  grid-template-columns: 35% 30% 35%;

  button {
    width: 100%;
    height: 5vh;
    border: 1px solid black;
    border-radius: 1em;
    background-color: white;
    font-size: 0.8rem;
    font-weight: bold;
    padding: 0 0.5em 0 0.5em;

    :hover {
      background-color: darkgrey;
      color: white;
    }
  }
}

h3 {
  height: 5vh;
  font-weight: bold;
  font-size: 0.8rem;
  letter-spacing: 5px;
}

@media only screen and (min-width: 600px) {
  #upload-form {
    margin-top: 4em;

    h3 {
      font-size: 1.2rem;
      margin-left: 3em;
    }

    .input {
      font-size: 1rem;
    }
  }

  .upload-image {
    width: 100%;
    margin-left: 2em;
  }

  .preview {
    img {
      height: 200px;
    }
  }
  .submit-btn {
    button {
      width: 90%;
      font-size: 1.2rem;
    }
  }

  h3 {
    font-size: 1rem;
  }
}

@media only screen and (min-width: 1024px) {
  #upload-form {
    margin-top: 2em;
    padding-top: 0.5em;

    h3 {
      font-size: 1rem;
      margin-left: 3em;
    }

    .input {
      margin: 0 0 0.5em 0;
      font-size: 0.8rem;
    }
  }

  .upload-image {
    width: 100%;
    margin-left: 2em;
  }

  .preview {
    min-height:10vh;
    margin-top: 0.5em;

    img {
      height: 100px;
    }
  }
  .submit-btn {
    button {
      width: 90%;
      font-size: 1rem;
    }
  }

  h3 {
    font-size: 0.8rem;
  }
}
</style>