<template>
  <section class="container-principal">
    <img src="img\undraw_Current_location_re_j130.png" alt="LOCATION" class="location-icon">

    <section class="container">
    
    <div class="content">
      <h2>Buscar Endereço</h2>

      <div class="form-group">
      
          <input 
          type="text" 
          id="cep" 
          name="cep" 
          placeholder="Digite o CEP"
          v-model="endereco.cep"
          @keyup.enter="buscarCep"
          >
          <button 
          @click="buscarCep"
          class="btn"
          >
          Buscar
        </button>
      </div>

      <div class="endereco-info" >

        <div class="info">
          <label for="logradouro">Logradouro: </label>
          <span>{{this.endereco.logradouro}}</span>
        </div> 
        
        <div class="info">
          <label for="bairro">Bairro: </label>
          <span>{{this.endereco.bairro}}</span>
        </div>

        <div class="info">
          <label for="localidade">Localidade: </label>
          <span>{{this.endereco.localidade}}</span>
        </div>
       
        <div class="info">
          <label for="ud">UF: </label>
          <span>{{this.endereco.uf}}</span>
        </div>

      </div>  
     
    </div>
   
  </section>

  </section>
  
  
  
</template>

<script>
export default {
  name: 'App',
  data(){
      return{
        endereco:{
          cep:'',
          logradouro:'',
          bairro:'',
          localidade:'',
          uf:'',
         
        },
        erro:''
      };
  },
  methods:{
     async buscarCep(){
     
        try{
          const response = await fetch(`http://viacep.com.br/ws/${this.endereco.cep}/json/`)
          const data = await response.json();

          this.endereco.logradouro = data.logradouro;
          this.endereco.bairro = data.bairro;
          this.endereco.localidade = data.localidade;
          this.endereco.uf = data.uf;
          this.erro = '';

        }catch(error){
        
          console.log(error);
        }
      },
  },
} 
</script>

<style>
section{
  font-family:Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  align-items: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container-principal{
  display: flex;
  flex-direction: row;
}
#cep{
  width: 300px;
  height: 33px;
  padding: 5px;
  margin: 8px;
  border-radius: 4px;
  border: 1px solid #4f4f4f;
  font-size: 17px;
}
.btn{
  border: none;
  border-radius: 4px;
  width: 100px;
  height: 48px;
  color:#fff;
  font-size: 20px;
  padding: 5px;
  background-color: #4f4f4f;
  cursor: pointer;
  
}

.btn:hover{
  background-color: #7e7e7e;
  color: #f5f5f6;
  transition: .5s;
}
.container{
  display: flex;
  justify-content: center;
   align-items: center;
}
.content{
  text-align: center;
}
.form-group {
  margin-bottom: 20px;
  
}
.endereco-info {
 display: flex;
 flex-direction: column;
 align-items: flex-start;

}
.info{
  padding: 10px;
  margin-top: 10px;
  font-family:Tahoma, sans-serif;
}

.location-icon {
  width: 500px; /* Largura da imagem */
  height: auto; /* Altura automática para manter a proporção */
  margin-right: 20px; /* Espaçamento à direita da imagem */
}
  </style>

