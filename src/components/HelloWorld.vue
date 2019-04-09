<template>
  <div class="hello">
    <h1>Pokémon:</h1>
    <input type="text" v-model="input.pokemon" placeholder="Pokémon" />
    <button v-on:click="sendData()">Send</button>
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
                response: ""
            }
        },
        //https://pokeapi.co/api/v2/pokemon/12/
        methods: {
            sendData() {
                axios({ method: "GET", "url": `https://pokeapi.co/api/v2/pokemon/${this.input.pokemon}/`, "headers": { "content-type": "application/json" } }).then(result => {
                    this.response = result.data.abilities.map((ab)=> ab.ability.name).join(", ");
                }, error => {
                    console.error(error);
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
