<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      Busca de Operadoras de Saúde<br>

    </p>
   
    <p><input type="text" v-model="operadoras"></p>
    
    <p><button type = "button" id = "get" @click = "fetchAPIData">BUSCAR</button></p>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',

  data() {
    return {
      operadoras: '',
    };
  },

  props: {
    msg: String,
    
  },
  methods: {
        

        fetchAPIData( ) { 

          
            fetch("http://127.0.0.1:8000/operadoras/"+this.operadoras, {
                "method": "GET",
                "headers": {
                    'Access-Control-Allow-Origin': '*',
                    'Access-Control-Request-Method': '*',
                    'Accept':'*'
                }
            })
            .then(response => { 
                if(response.ok){
                    return response.json()    
                } else{
                    alert("Server returned " + response.status + " : " + response.statusText);
                }                
            })
            .then(response => {
                this.result = response.body; 
                this.responseAvailable = true;
            })
            .catch(err => {
                console.log(err);
            });

        }
    }
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
