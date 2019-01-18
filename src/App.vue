<template>
  <div id="app">
    <Header />
    <form>

    </form>
    <input type="text" v-model="search" name="search" placeholder="Search">
    <input type="submit" class="btn" value="Submit" v-on:click="lookUpFoGiphs">
    <Giphs v-bind:result="result" />

  </div>
</template>

<script>
import Header from './components/layout/Header';
import Giphs from './components/Giphs';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Header,
    Giphs
  },
  data(){
    return {
      result: null,
      search: ''
    }
  },
  methods: {
    lookUpFoGiphs(){
      axios
      .get(`http://api.giphy.com/v1/gifs/search?q=${this.search}&api_key=EwQCHDTYU2onchg4pwYQmRFRcugz5ySa&limit=20`)
      .then(res => this.result = res.data.data)
      .catch(err => alert(err));
      this.search = '';
    }
  }
}

</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  form {
    width: 100%;
  }
  input[type="text"]{
    width: 80%;
    padding: 5px;
  }
  input[type="submit"]{
    width: 20%;
  }
</style>
