<template>
  <div class="hello">
    <h1>Your IP is {{ ip }}</h1>
    <input type="text" v-model="input.firstname" placeholder="first name" />
    <button v-on:click="sendData()">Send</button>
    <br />
    <br />
    <textarea>{{ response }}</textarea>
  </div>
</template>

<script>
    import axios from "axios";

    export default {
        name: 'HelloWorld',
        data () {
            return {
                ip: "",
                input: {
                    firstname: "",
                },
                response: ""
            }
        },
        mounted() {
            axios({ method: "GET", "url": "https://httpbin.org/ip" }).then(result => {
                this.ip = result.data.origin;
            }, error => {
                console.error(error);
            });
        },
        methods: {
            sendData() {
                axios({ method: "POST", "url": "https://httpbin.org/post", "data": this.input, "headers": { "content-type": "application/json" } }).then(result => {
                    this.response = result.data;
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
