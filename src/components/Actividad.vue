<template>
  <div class="hello">
    <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-primary">
      <a class="navbar-brand" href="https://vuejs.org/">
        <img src="../assets/logo.png" alt="Vue logo" width="20px" height="20px">
        Actividad Vue
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
          <li class="nav-item" v-bind:class="[show == 'home' ? 'active' : '']"
          @click="changeSection('home')">
            <a class="nav-link">
              Home
              <span class="sr-only">(current)</span>
            </a>
          </li>
          <li class="nav-item" v-bind:class="[show == 'project' ? 'active' : '']"
          @click="changeSection('project')">
            <a class="nav-link">Projects</a>
          </li>
          <li class="nav-item" v-bind:class="[show == 'service' ? 'active' : '']"
          @click="changeSection('service')">
            <a class="nav-link">Services</a>
          </li>
        </ul>
      </div>
    </nav>
    <div class="container">
      <div class="row"></div>
      <div class="col-md-12">
        <div class="card" v-if="show == 'home'">
          <br>
          <span class="img-container">
            <img src="../assets/pic.jpg" height="400px" width="400px"/>
          </span>
          <br>
          <div>
            <a href="https://the-vala.github.io/Resume/">
              <Button class="btn btn-success">
                Go to virtual CV
              </Button>
            </a>
          </div>
          <br>
        </div>
        <div class="card" v-if="show == 'project'">
          <h2>Projects</h2>
          <div class="col-md-12">
            <Button class="btn btn-success" @click="switchList">
              {{this.list ? "Grid" : "List"}}
            </Button>
          </div>
          <br>
          <ul class="list-group" v-if="list">
            <li class="list-group-item list-group-item-light vue-list"
            v-for="elem in listElem" :key="elem.text">
              <span>
                  <img :src="getImgUrl(elem.img)"
                  alt="Vue logo" width="70px" height="70px">
                  {{ elem.text }}
              </span>
            </li>
          </ul>
          <table v-if="!list">
            <tr>
              <td>
                <img src="../assets/swift.jpg"
                    alt="Swift logo" width="100px" height="100px">
                    <p>Swift</p>
              </td>
              <td>
                <img src="../assets/midi.jpg"
                    alt="Midi logo" width="100px" height="100px">
                    <p>Midi</p>
              </td>
            </tr>
            <tr>
              <td>
                <img src="../assets/php.jpg"
                    alt="PHP logo" width="100px" height="100px">
                    <p>PHP</p>
              </td>
              <td>
                <img src="../assets/html.jpg"
                    alt="HTML logo" width="100px" height="100px">
                    <p>HTML</p>
              </td>
            </tr>
          </table>
          <br>
        </div>
        <div class="card" v-if="show == 'service'">
          <h2>Services</h2>
          <ul class="list-group" v-if="list">
            <li class="list-group-item vue-list" @click="refreshSum(elem.text)"
            v-bind:class=
            "[elem.set ? 'list-group-item-success' : 'list-group-item-danger']"
            v-for="elem in sumElem" :key="elem.text">
              <span>{{ elem.text }} {{ elem.value }}</span>
            </li>
          </ul>
          <p>TOTAL: {{this.sum}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Actividad',
  data() {
    return {
      list: true,
      show: 'home',
      sum: 0,
      size: 100,
      listElem: [
        { text: 'Swift', img: 'swift.jpg' },
        { text: 'Web MIDI', img: 'midi.jpg' },
        { text: 'PHP', img: 'php.jpg' },
        { text: 'HTML', img: 'html.jpg' },
      ],
      sumElem: [
        { text: 'Web Development', value: 300, set: false },
        { text: 'Design', value: 400, set: false },
        { text: 'Integration', value: 250, set: false },
        { text: 'Training', value: 220, set: false },
      ],
    };
  },
  methods: {
    switchList() {
      event.preventDefault();
      this.list = !this.list;
    },
    refreshSum(text) {
      this.sum = 0;
      for (let i = 0; i < this.sumElem.length; i += 1) {
        if (this.sumElem[i].text === text) {
          this.sumElem[i].set = !this.sumElem[i].set;
        }
        if (this.sumElem[i].set) {
          this.sum += this.sumElem[i].value;
        }
      }
    },
    getImgUrl(logo) {
      const images = require.context('../assets/', false, /\.*$/);
      return images(`./${logo}`);
    },
    changeSection(section) {
      event.preventDefault();
      this.show = section;
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
  align-items: center;
  border: none !important;
}
table {
  margin: 10px;
}
.vue-list {
  width: 80%;
}
a {
  color: #42b983;
}
td {
  width: 50%;
  border-style: solid;
  border-color: darkgray;
  border-width: 1px;
}
.img-container {
  text-align: center;
}
</style>
