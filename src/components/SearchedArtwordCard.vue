<template>
  <div class="artwork-card">
    <div class="image">
      <img :src="art.url" alt="" />
    </div>
    <div class="description">
      <h3>{{ art.name }}</h3>
      <h4>{{ art.material }}</h4>
      <h4>{{ art.length }} X {{ art.width }}</h4>
      <h4>{{ art.completed_at }}</h4>
      <h4>{{ art.category }}</h4>
      <p>{{ art.status }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "artwork-card",
  data() {
    return {
      display: false,
    };
  },
  props: {
    art: {
      type: Object,
      required: true,
    },
  }
};
</script>

<style lang="scss" scoped>
.artwork-card {
  min-height: 50vh;
  width: 90%;
  display: grid;
  justify-items: center;
  align-items: start;
  align-content: start;
  border: 1px solid #aab8c2;
  row-gap: 1vh;
  margin: 0.5em;
}

.image {
  min-height: 30vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: start;
  margin-top: 1em;

  img {
    width: 90%;
    object-fit: cover;
  }
}

.description {
  height: 30vh;
  width: 100%;
  display: grid;
  justify-items: center;
  align-items: start;
  margin-top: 1em;

  h3 {
    width: 80%;
    height: 5vh;
    font-weight: bold;
    font-size: 1rem;
    margin-bottom: 0.5em;
  }

  h4 {
    font-size: 0.8rem;
    margin: 0 0.5em 0 0.5em;
    font-weight: normal;
  }

  p {
    margin: 0.5em;
    font-size: 0.8rem;
    text-align: center;
    background-color: grey;
    color: white;
    padding: 0.5em 0.8em 0.5em 0.8em;
  }
}

@media only screen and (min-width: 600px) {
  .image {
    margin-top: 2em;
  }

  .description {
    h3 {
      font-size: 1.5rem;
    }

    h4 {
      font-size: 1.2rem;
    }

    p {
      font-size: 1.2rem;
    }
  }
}

@media only screen and (min-width: 1024px) {
  .artwork-card {
    min-height: 100vh;
  }

  .image {
    margin-top: 2em;
  }

  .description {
    height: 40vh;
    h3 {
      font-size: 1.2rem;
      margin-bottom: 1.5em;
    }

    h4 {
      font-size: 1rem;
    }

    p {
      font-size: 1rem;
    }
  }
}
</style>