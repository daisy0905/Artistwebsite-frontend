<template>
  <div class="available-list">
    <div v-for="image in images" class="item" :key="image.id">
      <img :src="image.url" alt="" />
      <h4>{{ image.name }}</h4>
    </div>
  </div>
</template>

<script>
export default {
  name: "available",
  props: {
    Status: {
      type: String,
    },
  },
  data() {
    return {
      images: this.$store.getters.getAvailable,
    };
  },
  watch: {
    Status(newValue) {
      console.log(newValue);
      if (newValue == "available") {
        this.images = this.$store.getters.getAvailable;
        console.log(this.images);
      } else if (newValue == "onhold") {
        this.images = this.$store.getters.getOnhold;
        console.log(this.images);
      } else if (newValue == "sold") {
        this.images = this.$store.getters.getSold;
        console.log(this.images);
      }
    },
  },
  // computed: {
  //     images() {
  //         console.log(this.$store.getters.getAvailable);
  //         return this.$store.getters.getAvailable;
  //     }
  // },
};
</script>

<style lang="scss" scoped>
.available-list {
  min-height: 50vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: center;
}

.item {
  min-height: 10vh;
  width: 90%;
  display: grid;
  justify-items: left;
  align-items: center;
  grid-template-columns: 1.5fr 4fr;
  border-bottom: 1px solid lightgrey;

  h4 {
    font-size: 0.8rem;
    margin: 0 0.5em 0 1.2em;
    font-weight: normal;
    text-align: left;
  }

  img {
    margin: 0.2em 0 0.2em 0;
    height: auto;
    width: 85%;
  }
}

@media only screen and (min-width: 600px) {
  .item {
    grid-template-columns: 1fr 1fr;

    h4 {
      font-size: 1rem;
    }

    img {
      margin: 0.5em 0 0.5em 0;
    }
  }
}

@media only screen and (min-width: 1024px) {
  .item {
    min-height: 10vh;
    h4 {
      font-size: 1rem;
    }

    img {
      width: 80%;
    }

  }
}
</style>