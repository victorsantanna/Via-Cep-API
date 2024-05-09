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

      <div class="endereco-info" v-if="esconderInfo" >

        <div class="info">
          <label for="logradouro">Logradouro: </label>
          <input type="text" name="logradouro" id="logradouro" v-model="endereco.logradouro" class="input-info">
        </div> 
        
        <div class="info">
          <label for="bairro">Bairro: </label>
          <input type="text" name="bairro" id="bairro" v-model="endereco.bairro" class="input-info">
        </div>

        <div class="info">
          <label for="localidade">Localidade: </label>
          <input type="text" name="localidade" id="localidade" v-model="endereco.localidade" class="input-info">
        </div>
       
        <div class="info">
          <label for="ud">UF: </label>
          <input type="text" name="uf" id="uf" v-model="endereco.uf" class="input-info">
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
        esconderInfo:false
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
          this.esconderInfo = true;

        }catch(error){
        
          console.log(error);
        }
      },
  },
} 
</script>

<style>
body{
  
}
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
  margin-left: 20px;
  font-family:Tahoma, sans-serif;
}

.location-icon {
  width: 400px;
  height: auto; 
  margin-right: 20px;
  border-radius: 300px;
}
.input-info {
  width: 256px;
  height: 20px;
  border-top: 3px solid #4f4f4f;
  border-radius: 5px;
  font-family: Tahoma, Verdana, sans-serif;
  font-size: 15px;
} 
#uf{
  width: 330px;
}
#bairro{
  width:298px ;
}
#logradouro{
  width: 255px ;
}
label{
  font-family: Verdana, Tahoma, sans-serif;
  font-weight: bold;
}

</style>

