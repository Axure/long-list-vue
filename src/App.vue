<template>
  <div id="app">
    <img src="./assets/logo.png">
    <template v-for="(v, i) in slices">
      <HelloWorld msg="Welcome to Your Vue.js App" :key="i" :data="slice(i)" :handler="setValue" :slice="i"/>
    </template>
  </div>
</template>

<script>
  import HelloWorld from './components/HelloWorld.vue'

  export default {
    name: 'app',
    components: {
      HelloWorld
    },
    data(){
      return {
        elements: new Array(80000).fill(0).map(() => Math.random() * 1000 | 1)
      }
    },
    computed: {
      slices(){
        return new Array(Math.ceil(this.elements.length / 1000)).fill(0).map((e, i) => i);
      },
    },
    methods: {
      slice(i){
        return this.elements.slice(i * 1000, (i + 1) * 1000)
      },
      setValue(i, value){
        console.log(this, 'we are dealing with');
        this.$set(this.elements, i, value);
        // this.elements = this.elements.slice();
        console.log(this.elements)
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
    margin-top: 60px;
  }
</style>
