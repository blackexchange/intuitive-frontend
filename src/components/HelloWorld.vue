<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      Busca de Operadoras de Saúde<br>

    </p>
   
    <p><input type="text" v-model="operadoras"></p>
    
    <p><button type = "button" id = "get" @click = "fetchAPIData">BUSCAR</button></p>
    <h4>Relação</h4>
    <table class="table table-striped table-bordered">
            <thead>
                <tr>
                    <th>Registro</th>
                    <th>Razão Social</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="row in opList" :key="row.Registro_ANS">
                    <td>{{row.Registro_ANS}}</td>
                    <td>{{row.Razao_Social}}</td>
                </tr>
            </tbody>
        </table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  result:"",
  responseAvailable:false,

  data() {
    return {
      operadoras: '',
      listaOperadoras:[],
      opList: [
                { Registro_ANS: '-', Razao_Social: '-'}
              
            ]
    };
  },

  props: {
    msg: String,
    
  },
  methods: {
        

        fetchAPIData( ) { 

          
            fetch("http://18.204.14.178/operadoras/"+this.operadoras, {
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
                this.result = response; 
                this.opList = this.result['operadoras']
                console.log(this.opList)
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
