<template>
  <div class="hello">
    <p>Search Pokémon's abilities:</p>
    <input type="text" v-on:input="sendData()" v-model="input.pokemon" placeholder="Pokémon" />
    <br />
    <br />
    <pre>{{ response }}</pre>
  </div>
</template>

<script>
    import axios from "axios";

    export default {
        name: 'HelloWorld',
        data () {
            return {
                input: {
                    pokemon: "",
                },
                response: "",
                cache: {}
            }
        },
        methods: {
            sendData() {
              if(this.cache[this.input.pokemon])
              {
                this.response=this.cache[this.input.pokemon];
                return
              }

              if(this.input.pokemon.length < 3)
              return;
                axios({ method: "GET", "url": `https://pokeapi.co/api/v2/pokemon/${this.input.pokemon}/`, "headers": { "content-type": "application/json" } }).then(result => {
                    this.response = "Abilities: " + result.data.abilities.map((ab)=> ab.ability.name).join(", ");
                    this.cache[this.input.pokemon]=this.response
                }, error => {
                  this.response=`Did not find: ${this.input.pokemon}`;
                  this.cache[this.input.pokemon]=this.response

                    // console.error(error);
                });
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
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
