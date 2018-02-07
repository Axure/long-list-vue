<template>
  <div class="hello">
    <div>{{msg}}</div>
    <button v-on:click="append">append manually</button>
    <ul>
      <li v-for="(hehe, i) in displayList" v-bind:key="hehe">
        {{hehe}}
        <input  v-model="haha[i]"/>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    props: {
      msg: String,
    },
    data: () => ({
      haha: new Array(8000).fill(0).map((e, i) => i),
      displayList: []
    }),
    methods: {
      append(){
        console.log('We are appending');
        const length = this.displayList.length;
        this.displayList = this.displayList.concat(this.haha.slice(length, length + 1000));
        if (this.displayList.length < this.haha.length){
          requestAnimationFrame(() =>{
            this.append();
          })
        }
      }
    },
    computed: {}
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h3 {
    margin: 40px 0 0;
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
