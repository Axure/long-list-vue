<template>
  <div class="hello">
    <div>{{msg}}</div>
    <button v-on:click="append">append manually</button>
    <ul>
      <li v-for="(hehe, i) in displayList" v-bind:key="i">
        {{hehe}}
        <input v-on:keyup="setValue(i + slice * 1000, 1)"/>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    props: {
      msg: String,
      slice: Number,
      data: Array,
      handler: Function
    },
    data: () => ({
      displayList: []
    }),
    watch: {
      data: function() {
        this.displayList = [];
        this.append();
      }
    },
    methods: {
      append(){
        console.log('We are appending');
        const length = this.displayList.length;
        this.displayList = this.displayList.concat(this.data.slice(length, length + 1000));
        if (this.displayList.length < this.data.length){
          requestAnimationFrame(() =>{
            this.append();
          })
        }
      },
      setValue(i, value) {
        console.log('We are setting the value');
        this.handler(i, value);
      }
    },
    computed: {},
    mounted() {
      this.append();
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
