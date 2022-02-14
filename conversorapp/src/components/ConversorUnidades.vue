<template>
  <div id="container">

    <h1>{{cantidadFisica.name}}</h1>

    <div id="main">
        <input type="text" v-model="fromValue" placeholder="Ingresar la cantidad">
        <select v-model="fromUnit">
            <option v-for="unit in cantidadFisica.units" v-bind:key="unit"> {{unit}} </option>
        </select>
        <img src="https://icones.pro/wp-content/uploads/2021/06/symbole-fleche-droite-orange.png" width="50" height="50" viewBox="0 0 24 24" fill="rgb(77, 186, 135)">
        <p id="result">
            {{result}}
        </p> 
        <select v-model="resultUnit" placeholder="result">
            <option v-for="unit in cantidadFisica.units" v-bind:key="unit"> {{unit}} </option>
        </select>
    </div>
    <h2>El resultado de la conversión es: {{result}} {{resultUnit}}</h2>
    
    <img id="imagen" src="https://i.ytimg.com/vi/nqxHnu4LJ6k/maxresdefault.jpg" width="1300" height="500">
  </div>
</template>

<script>
export default {
  name: 'Converter',
  props: {
    cantidadFisica: Object  
  },
  data: function(){           
       return{
         fromValue:1,
         fromUnit:"",
         resultUnit:""
       }
  },
  methods:{
      toMinutes: function(value,fromUnit, resultUnit){   
        if(fromUnit=="Segundos" && resultUnit=="Segundos"){
             return value;
         } else if (fromUnit=="Segundos" && resultUnit =="Minutos"){
             return value/60;
         } else if (fromUnit=="Segundos" && resultUnit =="Horas"){
             return value/3600;
         } else if (fromUnit=="Minutos" && resultUnit =="Minutos"){
             return value;
         } else if (fromUnit=="Minutos" && resultUnit =="Segundos"){
             return value*60;
         } else if (fromUnit=="Minutos" && resultUnit =="Horas"){
             return value/60;
         } else if (fromUnit=="Horas" && resultUnit =="Horas"){
             return value;
         } else if (fromUnit=="Horas" && resultUnit =="Segundos"){
             return value*3600;
         } else if (fromUnit=="Horas" && resultUnit =="Minutos"){
             return value*60;    
        }
      },
      tologitud: function(value,fromUnit,resultUnit){
        if(fromUnit=="mm" && resultUnit=="mm"){
             return value;
         } else if (fromUnit=="mm" && resultUnit =="cm"){
             return value/10;
         } else if (fromUnit=="mm" && resultUnit =="m"){
             return value*0.001;
         } else if (fromUnit=="cm" && resultUnit =="cm"){
             return value;
         } else if (fromUnit=="cm" && resultUnit =="mm"){
             return value*10;
         } else if (fromUnit=="cm" && resultUnit =="m"){
             return value/100;
         } else if (fromUnit=="m" && resultUnit =="m"){
             return value;
         } else if (fromUnit=="m" && resultUnit =="mm"){
             return value/0.0010000;
         } else if (fromUnit=="m" && resultUnit =="cm"){
             return value*100;    
        }
      },
      toGigabytes: function(value,fromUnit,resultUnit){ 
        if(fromUnit=="Kilobytes" && resultUnit=="Kilobytes"){
             return value;
         } else if (fromUnit=="Kilobytes" && resultUnit =="Megabytes"){
             return value/1024;
         } else if (fromUnit=="Kilobytes" && resultUnit =="Gigabytes"){
             return (value/1024)/1024;
         } else if (fromUnit=="Megabytes" && resultUnit =="Megabytes"){
             return value;
         } else if (fromUnit=="Megabytes" && resultUnit =="Kilobytes"){
             return value*1024;
         } else if (fromUnit=="Megabytes" && resultUnit =="Gigabytes"){
             return value/1024;
         } else if (fromUnit=="Gigabytes" && resultUnit =="Gigabytes"){
             return value;
         } else if (fromUnit=="Gigabytes" && resultUnit =="Kilobytes"){
             return (value*1024)*1024;
         } else if (fromUnit=="Gigabytes" && resultUnit =="Megabytes"){
             return value*1024;    
        }
      },
      toDolar: function(value,fromUnit,resultUnit){
         if(fromUnit=="Colones" && resultUnit=="Colones"){
             return value;
         } else if (fromUnit=="Colones" && resultUnit =="Dolares"){
             return value*0.11;
         } else if (fromUnit=="Colones" && resultUnit =="Euros"){
             return value*0.10;
         } else if (fromUnit=="Dolares" && resultUnit =="Colones"){
             return value*8.79;
         } else if (fromUnit=="Dolares" && resultUnit =="Dolares"){
             return value;
         } else if (fromUnit=="Dolares" && resultUnit =="Euros"){
             return value*0.88206831;
         } else if (fromUnit=="Euros" && resultUnit =="Colones"){
             return value*9.97;
         } else if (fromUnit=="Euros" && resultUnit =="Dolares"){
             return value*1.14;
         } else if (fromUnit=="Euros" && resultUnit =="Euros"){
             return value;    
        }
      },
        toMasa: function(value,fromUnit,resultUnit){
         if(fromUnit=="kg" && resultUnit=="kg"){
             return value;
         } else if (fromUnit=="kg" && resultUnit =="g"){
             return value*1000;
         } else if (fromUnit=="kg" && resultUnit =="mg"){
             return value*1000000;
         } else if (fromUnit=="g" && resultUnit =="kg"){
             return value/1000;
         } else if (fromUnit=="g" && resultUnit =="g"){
             return value;
         } else if (fromUnit=="g" && resultUnit =="mg"){
             return value*1000;
         } else if (fromUnit=="mg" && resultUnit =="kg"){
             return value/1000000;
         } else if (fromUnit=="mg" && resultUnit =="g"){
             return value/1000;
         } else if (fromUnit=="mg" && resultUnit =="mg"){
             return value;    
        }
      }

  },


  computed: {           
      result: function(){
            let value = parseFloat(this.fromValue);  
            if(isFinite(value)){                     

              switch(this.cantidadFisica.name){    
                case("Tiempo"): {
                        let valueInMinutes = this.toMinutes(value,this.fromUnit,this.resultUnit);
                        switch(this.resultUnit){
                        case("Segundos"):
                            return parseFloat((valueInMinutes).toFixed(5));   
                        case("Minutos"):
                            return parseFloat((valueInMinutes).toFixed(5));
                        case("Horas"):
                            return parseFloat((valueInMinutes).toFixed(5));
                        default:
                            console.log("Error detectado - unidad no seleccionada");
                            return "...";
                        }
                }
                case("Longitud"): {
                   
                        let valuelon= this.tologitud(value,this.fromUnit,this.resultUnit); 
                        switch(this.resultUnit){
                        case("mm"):
                            return parseFloat((valuelon).toFixed(10));   
                        case("cm"):
                            return parseFloat((valuelon).toFixed(10));
                        case("m"):
                            return parseFloat((valuelon).toFixed(10));
                        default:
                            console.log();
                            return "...";
                        }
                 }
                 case("Almacenamiento"): {
                        let valueAlma= this.toGigabytes(value,this.fromUnit,this.resultUnit);
                        switch(this.resultUnit){
                        case("Kilobytes"):
                            return parseFloat((valueAlma).toFixed(10));   
                        case("Megabytes"):
                            return parseFloat((valueAlma).toFixed(10));
                        case("Gigabytes"):
                            return parseFloat((valueAlma).toFixed(10));
                        default:
                            console.log("");
                            return "...";
                        }
                  }
                  case("Monedas"): {
                    //Conversiones con tiempo
                        let valueInMonedas = this.toDolar(value,this.fromUnit,this.resultUnit);  // we use "minutes" as an intermediary unit
                        switch(this.resultUnit){
                        case("Colones"):
                            return parseFloat((valueInMonedas).toFixed(2));   // limit to 5 decimals and parseFloat() it to remove redundant 0s
                        case("Dolares"):
                            return parseFloat((valueInMonedas).toFixed(2));
                        case("Euros"):
                            return parseFloat((valueInMonedas).toFixed(2));
                        default:
                            console.log("Error detectado - unidad no seleccionada");
                    }        return "...";
                 }
   
                  /* ----------------------------*/
                  case("Masa"): {
                    //Conversiones con Masa
                        let valueInMasa = this.toMasa(value,this.fromUnit,this.resultUnit);  // we use "minutes" as an intermediary unit
                        switch(this.resultUnit){
                        case("kg"):
                            return parseFloat((valueInMasa).toFixed(8));   // limit to 5 decimals and parseFloat() it to remove redundant 0s
                        case("g"):
                            return parseFloat((valueInMasa).toFixed(3));
                        case("mg"):
                            return parseFloat((valueInMasa).toFixed(3));
                        default:
                            console.log("Error detectado - unidad no seleccionada");
                            return "...";
                        }
                  }

              }
            }      
            return "...";  
      }
  }
}
</script>

<style scoped>
  #container{
    width:80vw;
    color:rgb(20,20,20);
    height:100vh;
    display:flex;
    flex-direction:column;
    justify-content:flex-start;
  }
  h1{
    width:100%;
    background-color:#73848f;
    box-sizing:border-box;
    padding:40px;
    color: rgb(255, 255, 255);
  }

  h2{
    width:100%;
    background-color:#73848f;
    box-sizing:border-box;
    padding:10px;
    color: rgb(255, 255, 255);
  }

  #main{
    display:flex;
    box-sizing:border-box;
    padding:40px;
    padding-left: 300px;
  }
  
  #main>*{
    margin:0 5px 0 5px;
  }
  input,select{
    padding:10px;
    border: 2px solid rgb(223, 113, 62);
    border-radius:10px;
    width:10vw;
    font-family:"Source Sans Pro";
    font-size:1em;
    display:flex;
    align-items:center;
  }
  #result{
    padding:10px;
    border: 2px solid rgb(223, 113, 62);
    border-radius:10px;
    width:10vw;
    font-family:"Source Sans Pro";
    font-size:1em;
    display:flex;
    align-items:center;
    background-color: white;
  }
  #imagen{
    box-sizing:border-box;
    display: block;   
    margin: auto;
    }
</style>