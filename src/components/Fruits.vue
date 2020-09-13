<template>
  <div class="hello">
    <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-primary">
      <a class="navbar-brand" href="https://vuejs.org/">
        <img src="../assets/logo.png" alt="Vue logo" width="20px" height="20px">
        Ejercicio Vue
      </a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarsExampleDefault"
        aria-controls="navbarsExampleDefault"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarsExampleDefault">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="https://www.google.com/">
              Let's Google
              <span class="sr-only">(current)</span>
            </a>
          </li>
          <li class="nav-item dropdown">
            <a
              class="nav-link dropdown-toggle"
              href="#"
              id="dropdown01"
              data-toggle="dropdown"
              aria-haspopup="true"
              aria-expanded="false">
              List
            </a>
            <div class="dropdown-menu" aria-labelledby="dropdown01">
              <a class="dropdown-item" href="#">Item 1</a>
              <a class="dropdown-item" href="#">Item 2</a>
              <a class="dropdown-item" href="#">Item 3</a>
            </div>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="https://github.com/the-vala/vue-practice">Link to Repo</a>
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <input class="form-control mr-sm-2" type="text"
          placeholder="Search" aria-label="Search" />
          <button class="btn btn-success my-2 my-sm-0" type="submit">Go</button>
        </form>
      </div>
    </nav>
    <h1>Fruit Pic</h1>
    <div class="container">
      <div class="row"></div>
      <div>
        <Button class="btn btn-success" @click="showImage">
          {{show ? "Hide Pic" : "Show Pic"}}
        </Button>
        <Button class="btn btn-success" @click="changeImage">Change Pic</Button>
      </div>
      <div class="col-md-12">
        <div class="card" v-if="show">
          <img :src="getImgUrl(selectedImage)" :height="size" :width="size"/>
          <v-card-text>
          <v-slider
            v-model="size"
            append-icon="zoom_in"
            prepend-icon="zoom_out"
            @click:append="increaseSize"
            @click:prepend="reduceSize"></v-slider>
        </v-card-text>
        </div>
      </div>
      <br>
      <div class="col-md-12">
        <h2 v-bind:title="hoverMessage">
          Dynamically Bound Title (Hover)
        </h2>
      </div>
      <br>
      <div class="col-md-12">
        <div class="card">
          <h1>2 Way Binded Message</h1>
          <span>
            <textarea v-model="inputMessage" placeholder="Your message"></textarea>
          </span>
          <p>Message: {{ inputMessage }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const fruits = ['fruits.jpg', 'apple.jpg', 'banana.jpg', 'watermelon.jpg', 'strawberry.jpg'];
export default {
  name: 'Fruits',
  data() {
    return {
      selectedImage: fruits[0],
      hoverMessage: `Today is ${new Date().toLocaleString()}`,
      inputMessage: '',
      show: true,
      size: 100,
    };
  },
  methods: {
    showImage(event) {
      event.preventDefault();
      if (event) {
        this.$set(this.$data, 'show', !this.show);
      }
    },
    getImgUrl(fruit) {
      const images = require.context('../assets/', false, /\.*$/);
      return images(`./${fruit}`);
    },
    changeImage(event) {
      event.preventDefault();
      if (event) {
        this.$set(
          this.$data,
          'selectedImage',
          fruits[Math.ceil(Math.random() * (5)) - 1],
        );
      }
    },
    reduceSize() {
      this.size = (this.size - 100) || 100;
    },
    increaseSize() {
      this.size = (this.size + 100) || 1000;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
