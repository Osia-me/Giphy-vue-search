<template>
  <div>
    <ul class="giphs">
      <template v-for="item in result">
        <li class="giph">
          <input type="checkbox" id="checkbox" v-bind:value="item.images.original.url" v-model="faveImages">
          <label for="checkbox"><img class="img" v-bind:src="item.images.original.url" v-bind:alt="item.title"></label>
        </li>
      </template>
    </ul>

      <br>
      <hr>
      <h1>Here is your favorites</h1>
      <ul class="giphs">
      <template v-for="item in faveImages">
        <li class="giph">
          <img class="img" v-bind:src="item" v-bind:alt="item"></label>
        </li>
      </template>
    </ul>
  </div>
</template>

<script>

export default {
  name: "giphs",
  props: ["result"],
  data(){
    return {
      favorite: [],
      faveImages: []
    }
  },
  watch: {
  faveImages: {
    handler() {
      console.log('Added fave!');
      localStorage.setItem('faveImage', JSON.stringify(this.faveImages));
    },
    deep: true,
  },
},
  mounted() {
    console.log('App mounted!');
    if (localStorage.getItem('faveImage')) this.faveImages = JSON.parse(localStorage.getItem('faveImage'));
  },
}
</script>

<style lang="css" scoped>
.giphs {
  margin: 10px;
  text-align: center;
}
.giph {
  display: inline-block;
}
.img {
  width: 350px;
  height: 250px;
  margin-right: 10px;
}
  img {
  position: relative;
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 5px;
  width: 150px;
  }

  img:hover {
    box-shadow: 0 0 2px 1px rgba(0, 140, 186, 0.5);
  }

  h1 {
    text-align: center;
  }

  input{
    display: inline-block;
    position: absolute;
    z-index: 1;
    width:20px;
    height:20px;
  }

</style>
