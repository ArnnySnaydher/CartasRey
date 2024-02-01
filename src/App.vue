<script setup>
import { computed, ref } from "vue";
import { productos } from "./datos";

//Imagen
const imageRey = "https://www.html6.es/img/rey_";
const logo="oferta.jpg"
//valor reactivo
let contador = ref(1);
let limite = 7;
const vuelta = () => {
  if (contador.value < limite) {
    contador.value++;
  } else {
    contador.value = 1;
  }

};

//propiedad computada
let name = computed(()=>{
  let nameRey = productos[contador.value-1].nombre.toLowerCase()
  return nameRey.substring(0,1).toUpperCase()+nameRey.substring(1)
})

let imagen = computed(()=>{

  return imageRey + productos[contador.value-1].nombre.toLocaleLowerCase() + ".png"
})

let precio = computed(()=>{
  let decimal = productos[contador.value-1].precio*0.10
return decimal.toFixed(2) + "€"
})

</script>
<template>
  <div class="borde">
    <div class="encabezado">
      <h2 >Cena {{ contador }} con el rey godo {{ name }}</h2>
    </div>
    <div class="etiqueta">
      <p class="">Precio: {{productos[contador-1].precio}} €</p>
      <span v-if="productos[contador-1].finDeSemana" class="verde">(De lunes a domingo)</span>
      <span v-else="productos[contador-1].finDeSemana" class="rojo">(Solo fines de semana)</span>
     </div> 
      <div v-if="productos[contador-1].precio < 100" class="descuento">
        <p>Ahorra un 10% dto: {{precio}} <img :src="logo" alt="" class="logo" /></p>
      </div>
    
    <div class="centro">
      <img :src="imagen" alt="" />
      <button class="boton" @click="vuelta()">
        Siguiente ({{ contador }}/7)
      </button>
    </div>
  </div>
</template>

<style>
.borde {
  border: 3px solid #333;
  border-radius: 0.5cm;
  margin: 10px;
  padding: 20%;
  padding-top: 0%;
  text-align: center;
  position: absolute;
 
}
.etiqueta{
  margin-top: 20%;

}

img {
  display: block;
  margin: auto;
  max-width: 100%;
  height: auto;
  margin-top: 10%;
  

}

.boton {
  position: absolute;
  bottom: 10px; 
  left: 50%; 
  transform: translateX(-50%); /* Centra el botón utilizando transformación */
  padding: 10px 20px; 
  
}
.descuento{
  display: inline;
}

.verde{
  background-color: green;
  padding: 3px 20px;
  border-radius: 5px;
  color: aliceblue;
}

.rojo{
  background-color: red;
  padding: 3px 20px;
  border-radius: 5px;
  color: aliceblue;
}
.logo{
  width: auto;
  margin: 0;
  height: 30px;
  display: inline-flex;
  transform: translateY(+30%)
}
.encabezado{
  position: absolute;
}

</style>
