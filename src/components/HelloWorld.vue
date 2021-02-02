<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div>{{myData}}</div>
    <hr>
    <div>{{myChars}}</div>
    <hr> 
    <div>{{myVars}}</div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data () {
    return {
      myData: {},
      myChars: {},
      myVars: {}
    }
  },
  async mounted() {   
    this.myData = await (await fetch('https://swapi.dev/api/planets/3/')).json()

    this.myChars = await (await fetch('https://rickandmortyapi.com/graphql',
    {
      method: 'POST',
      headers: {'Content-Type': 'application/json'},
      body: JSON.stringify({
        query: `{
          characters() {
            results {
              name
            }
          }
        }`
      })
    })).json()

    this.myVars = await (await fetch('/CohortsCentral/catalogue/graphql',
     {
      method: 'POST',
      headers: {'Content-Type': 'application/json'},
      body: JSON.stringify({
        query: `{
          Variables(limit: 10) {
            name
            description
            label
            unit{
              name
            }
          }
        }`
      })
    })).json()

  },
});
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
