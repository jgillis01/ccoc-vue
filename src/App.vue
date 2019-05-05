<template>
  <div id="app" class="col-12">
    <input type="text" class="col-12" v-model="searchString" placeholder="Date or Author or Title Search"/>
    <ul class="col-12">
      <li class="col-12" v-for="recording in filteredRecordings">
        <a :href="recording.htmlPath">{{recording.date}} - {{recording.author}} - {{recording.title}}</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      recordings: [],
      searchString: ''
    }
  },
  created () {
    this.$http.get('/recordings.json').then(function (data) {
      this.recordings = data.body
    })
  },
  computed: {
    filteredRecordings: function () {
      return this.recordings.filter((recording) => {
        return recording.title.match(this.searchString) || recording.author.match(this.searchString) || recording.date.match(this.searchString)
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
ul {
  margin-top: 20px;
}
ul > li {
  list-style: none;
  text-align: left;
}
input {
  width: 20em;
}
</style>
