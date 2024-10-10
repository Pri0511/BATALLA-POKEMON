<template>
  <div class="conten">
<!-- Overlay Modal -->
<div v-if="showOverlay" class="overlay">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="exampleModalLabel">Número de Rondas</h1>
          
          </div>
          <div class="modal-body">
            <input type="number" v-model="rondasInput" class="form-control" placeholder="Ingrese el número de rondas" />
          </div>
          <div class="modal-footer">
  
            <button type="button" class="btn btn-custom" @click="setRondas">Guardar cambios</button>
          </div>
        </div>
      </div>
    </div>

    
    <!-- primer jugador -->
    <div class="contenedor">
      <div class="parte2">
        <div class="contenedorparte2">
          <div class="cont2_1">
            <div class="nom">
              <h1 :class="{ 'not-found': nombre1 === 'Pokémon no encontrado' }">
                {{ nombre1 !== 'Pokémon no encontrado' ? nombre1 : 'Pokémon no encontrado' }}
              </h1>
            </div>
            <div class="num">
              <h1>{{ num1 }}</h1>
            </div>
          </div>
          <div class="cont2_2">
            <div class="cara1" :class="{ 'default-image': nombre1 === 'Pokémon no encontrado' }"
              :style="{ backgroundColor: tipos1.length > 0 ? typeColors[tipos1[0]] : 'rgba(224, 217, 217, 0.363)' }">
              <img :src="image1" alt="">
            </div>
            <div class="cara2">
              <div class="tipo1">Tipo:</div>
              <div class="tipo2">
                <button v-for="tipo in tipos1" :key="tipo" class="btn-tipo"
                  :style="{ backgroundColor: typeColors[tipo] }">
                  {{ tipo }}</button>
              </div>
            </div>
            <div class="cara3">
              <div class="debilidades1">Debilidad:</div>
              <div class="debilidades2">
                <button v-for="debilidad in debilidades1" :key="debilidad" class="btn-debilidad"
                  :style="{ backgroundColor: weaknessColors[debilidad] }">{{ debilidad }}</button>
              </div>
            </div>
          </div>
          <div class="cont2_3">
            <div class="column1">
              <div class="fila1">Base</div>
              <div class="fila2">HP:</div>
              <div class="fila3">Attack:</div>
              <div class="fila4">Defense:</div>
              <div class="fila5">Sp.Attack:</div>
              <div class="fila6">Sp.Defense:</div>
              <div class="fila7">Speed:</div>
            </div>
            <div class="column2">
              <div class="fila8">Stats</div>
              <div class="fila9">{{ hp1 }}</div>
              <div class="fila10">{{ Attack1 }}</div>
              <div class="fila11">{{ Defense1 }}</div>
              <div class="fila12">{{ SpAttack1 }}</div>
              <div class="fila13">{{ SpDefense1 }}</div>
              <div class="fila14">{{ Speed1 }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- parte de la mitad -->
    <div class="contenedormitad">
      <div class="partemitad">
        <div class="partemitad_1">
          <label id="pide1" for="numero">ronda:</label>
          {{ ronda }}
        </div>
        <div class="partemitad_2">
          <div id="cara1mitad">
          </div>
          <div id="results"></div>
        </div>
        <div class="partemitad_3">
          <div class="img_ganador"
          :style="{ backgroundColor: colorGanador.length > 0 ? typeColors[colorGanador[0]] : 'rgba(224, 217, 217, 0.363)' }">
          
          <img id="fotoo" v-if="imgMaxGanador" :src="imgMaxGanador" alt="Imagen del ganador con más rondas">
          <h1>Pokemon con mayor puntaje: {{ nombreGanador }}</h1>
        </div>
          <div class="partebutton">
            <button class="recarga" @click="generarcomparar" :disabled="ronda >= totalRondas"> SIGUIENTE</button>
          </div>
          

        </div>
      </div>

    </div>
    <!-- Segundo jugador -->
    <div class="contenedor2">
      <div class="parte2">
        <div class="contenedorparte2">
          <div class="cont2_1">
            <div class="nom">
              <h1 :class="{ 'not-found': nombre2 === 'Pokémon no encontrado' }">
                {{ nombre2 !== 'Pokémon no encontrado' ? nombre2 : 'Pokémon no encontrado' }}
              </h1>
            </div>
            <div class="num">
              <h1>{{ num2 }}</h1>
            </div>
          </div>
          <div class="cont2_2">
            <div class="cara1" :class="{ 'default-image': nombre2 === 'Pokémon no encontrado' }"
              :style="{ backgroundColor: tipos2.length > 0 ? typeColors[tipos2[0]] : 'rgba(224, 217, 217, 0.363)' }">
              <img :src="image2" alt="">
            </div>
            <div class="cara2">
              <div class="tipo1">Tipo:</div>
              <div class="tipo2">
                <button v-for="tipo in tipos2" :key="tipo" class="btn-tipo"
                  :style="{ backgroundColor: typeColors[tipo] }">
                  {{ tipo }}</button>
              </div>
            </div>
            <div class="cara3">
              <div class="debilidades1">Debilidad:</div>
              <div class="debilidades2">
                <button v-for="debilidad in debilidades2" :key="debilidad" class="btn-debilidad"
                  :style="{ backgroundColor: weaknessColors[debilidad] }">{{ debilidad }}</button>
              </div>
            </div>
          </div>
          <div class="cont2_3">
            <div class="column1">
              <div class="fila1">Base</div>
              <div class="fila2">HP:</div>
              <div class="fila3">Attack:</div>
              <div class="fila4">Defense:</div>
              <div class="fila5">Sp.Attack:</div>
              <div class="fila6">Sp.Defense:</div>
              <div class="fila7">Speed:</div>
            </div>
            <div class="column2">
              <div class="fila8">Stats</div>
              <div class="fila9">{{ hp2 }}</div>
              <div class="fila10">{{ Attack2 }}</div>
              <div class="fila11">{{ Defense2 }}</div>
              <div class="fila12">{{ SpAttack2 }}</div>
              <div class="fila13">{{ SpDefense2 }}</div>
              <div class="fila14">{{ Speed2 }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>



  </div>
</template>
<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const typeColors = {
  normal: '#A8A878',
  fire: '#F08030',
  water: '#6890F0',
  electric: '#F8D030',
  grass: '#78C850',
  ice: '#98D8D8',
  fighting: '#C03028',
  poison: '#A040A0',
  ground: '#E0C068',
  flying: '#A890F0',
  psychic: '#F85888',
  bug: '#A8B820',
  rock: '#B8A038',
  ghost: '#705898',
  dragon: '#7038F8',
  dark: '#705848',
  steel: '#B8B8D0',
  fairy: '#EE99AC'
};

const weaknessColors = {
  normal: '#A8A878',
  fire: '#F08030',
  water: '#6890F0',
  electric: '#F8D030',
  grass: '#78C850',
  ice: '#98D8D8',
  fighting: '#C03028',
  poison: '#A040A0',
  ground: '#E0C068',
  flying: '#A890F0',
  psychic: '#F85888',
  bug: '#A8B820',
  rock: '#B8A038',
  ghost: '#705898',
  dragon: '#7038F8',
  dark: '#705848',
  steel: '#B8B8D0',
  fairy: '#EE99AC'
};

let nombre1 = ref("");
let image1 = ref("");
let num1 = ref("");
let hp1 = ref("");
let Attack1 = ref("");
let Defense1 = ref("");
let SpAttack1 = ref("");
let SpDefense1 = ref("");
let Speed1 = ref("");
let tipos1 = ref([]);
let debilidades1 = ref([]);

let nombre2 = ref("");
let image2 = ref("");
let num2 = ref("");
let hp2 = ref("");
let Attack2 = ref("");
let Defense2 = ref("");
let SpAttack2 = ref("");
let SpDefense2 = ref("");
let Speed2 = ref("");
let tipos2 = ref([]);
let debilidades2 = ref([]);
let ronda = ref(0);
let ganador = ref("");
let colorGanador = ref("");
let nombreGanador= ref("");
let ganadorfijo = ref("");
const resultados = [];

let victorias = ref({
  [nombre1.value]: 0,
  [nombre2.value]: 0,
});

let maxGanador = ref(""); 
let imgMaxGanador = ref("");


let totalRondas = ref(5); 


const rondasInput = ref(0);
const showOverlay = ref(true); 
// Métodos
// Métodos
function setRondas() {
  if (rondasInput.value > 0) {
    totalRondas.value = rondasInput.value;
    ronda.value = 0;
    closeOverlay();
  }
}

function closeOverlay() {
  showOverlay.value = false;
}









async function generarcomparar() {

  ronda.value++;


  if (ronda.value === 1) {
    
    const randomId1 = Math.floor(Math.random() * 1025) + 1;
    const randomId2 = Math.floor(Math.random() * 1025) + 1;
    

    await listarPokemones(randomId1, true);
    await listarPokemones(randomId2, false);
  } else {
 
    if (Attack1.value > Attack2.value) {
  
      const randomId2 = Math.floor(Math.random() * 1025) + 1;
      await listarPokemones(randomId2, false); 
    } else if (Attack2.value > Attack1.value) {

      const randomId1 = Math.floor(Math.random() * 1025) + 1;
      await listarPokemones(randomId1, true); 
    }
  }


  if (Attack1.value > Attack2.value) {
    ganador.value = nombre1.value;
    ganadorfijo = nombre1.value;
    victorias.value[nombre1.value] = (victorias.value[nombre1.value] || 0) + 1; 
  } else if (Attack2.value > Attack1.value) {
    ganador.value = nombre2.value;
    ganadorfijo = nombre2.value;
    victorias.value[nombre2.value] = (victorias.value[nombre2.value] || 0) + 1; 
  } else {
    ganadorfijo = "Empate";
    ganador.value = "Empate";
  }


  console.log(`Ronda ${ronda.value}: ${nombre1.value} vs ${nombre2.value} - Ganador: ${ganadorfijo}`);


  let maxVictorias = 0;
  let pokemonMasGanadas = "";

  for (const [nombre, victoriasCount] of Object.entries(victorias.value)) {
    if (victoriasCount > maxVictorias) {
      maxVictorias = victoriasCount;
      pokemonMasGanadas = nombre;
    }
  }


  console.log(`El Pokémon con más rondas ganadas hasta ahora es: ${pokemonMasGanadas} con ${maxVictorias} victorias.`);

  
  if (pokemonMasGanadas === nombre1.value) {
    imgMaxGanador.value = image1.value;
    colorGanador.value = tipos1.value;
    nombreGanador.value = nombre1.value;
  } else if (pokemonMasGanadas === nombre2.value) {
    imgMaxGanador.value = image2.value;
    colorGanador.value = tipos2.value;
    nombreGanador.value = nombre2.value;
  }

 
  const resultado = `Ronda ${ronda.value}: ${nombre1.value} vs ${nombre2.value} - Ganador: ${ganadorfijo}`;
  resultados.push(resultado);
  renderResultados();
}

function renderResultados() {
  const resultsContainer = document.getElementById('results');
  resultsContainer.innerHTML = ''; 

  resultados.forEach((resultado, index) => {
    const div = document.createElement('div');
    div.className = 'round-result';
    div.innerText = resultado;
    resultsContainer.appendChild(div);
  });
}

async function listarPokemones(id, isFirst) {
  const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
  try {
    let { data } = await axios.get(url);
    if (isFirst == true) {
      nombre1.value = data.name;
      image1.value = data.sprites.front_default;
      num1.value = data.id;
      hp1.value = data.stats[0].base_stat;
      Attack1.value = data.stats[1].base_stat;
      Defense1.value = data.stats[2].base_stat;
      SpAttack1.value = data.stats[3].base_stat;
      SpDefense1.value = data.stats[4].base_stat;
      Speed1.value = data.stats[5].base_stat;
      tipos1.value = data.types.map(tipo => tipo.type.name);
      debilidades1.value = await obtenerDebilidades(data.types.map(tipo => tipo.type.name));
    } else {
      nombre2.value = data.name;
      image2.value = data.sprites.front_default;
      num2.value = data.id;
      hp2.value = data.stats[0].base_stat;
      Attack2.value = data.stats[1].base_stat;
      Defense2.value = data.stats[2].base_stat;
      SpAttack2.value = data.stats[3].base_stat;
      SpDefense2.value = data.stats[4].base_stat;
      Speed2.value = data.stats[5].base_stat;
      tipos2.value = data.types.map(tipo => tipo.type.name);
      debilidades2.value = await obtenerDebilidades(data.types.map(tipo => tipo.type.name));
    }

  } catch (error) {
    if (isFirst) {
      nombre1.value = "Pokémon no encontrado";
    } else {
      nombre2.value = "Pokémon no encontrado";
    }
  }
}

async function obtenerDebilidades(tipos) {
  let debilidades = [];
  for (let tipo of tipos) {
    let url = `https://pokeapi.co/api/v2/type/${tipo}`;
    let { data } = await axios.get(url);
    data.damage_relations.double_damage_from.forEach(d => {
      if (!debilidades.includes(d.name)) {
        debilidades.push(d.name);
      }
    });
  }
  return debilidades;
}

onMounted(() => {
  generarPokemonAleatorio();
});





</script>
<style>
#app,
body {
  height: 100vh;
  width: 100vw;
  margin-top: 0px;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url(https://i.pinimg.com/564x/30/3d/d3/303dd3e60c07e276720dc5221a308235.jpg);
  background-size: 100%;
  background-position: center;
  background-repeat: no-repeat;

}

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1050; 
}

.modal-dialog {
  background: rgba(88, 91, 92, 0.9);
  border-radius: 0.5rem;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  padding: 1rem;
}

.btn-custom {
  margin-top: 10px;
}

.conten {
  height: 100vh;
  width: 100vw;
  padding: 0;
  display: grid;
  grid-template-columns: 33.33% 33.33% 33.33%;
}


.contenedor,
.contenedor2,
.contenedormitad {
  margin-top: 20px;
  position: relative;
  width: 320px;
  height: 480px;
  display: grid;
  grid-template-rows: 4fr 1fr;
}

.contenedor {
  margin-left: 40px;
  margin-top: 60px;
}

.contenedormitad {
  margin-left: 20px;
  margin-top: 60px;
}

.contenedor2 {
  margin-left: 0px;
  margin-top: 60px;
}

.btn-tipo,
.btn-debilidad {

  max-height: 20px;
  width: 55px;
  margin: 1px;
  padding: 0px 2px;
  background-color: #ccc;
  color: rgb(255, 255, 255);
  max-width: 50px;
  font-size: 0.8rem;
}


.recarga {
  width: 120px;
  height: 35px; 
  padding: 0;
  margin-top: 10px;
  border-radius: 10px;
  background-color: transparent;
  border: none;
  outline: none;
}
/* ---------------------------------------------- */
.recarga:focus {
  outline: none;
  border: none;
  
}
.recarga:hover{
  background-color: rgba(224, 217, 217, 0.363);
}

div.cara1.default-image img {
  width: 100%;
  height: 100%;
  background-size: 20px;
  margin-top: 0px;
  border-radius: 10px;
}




h1.not-found {
  text-align: left;
  font-size: 0.7rem;
  margin-left: 25%;
  margin-top: 1px;
  color: rgb(49, 49, 49);
}

.contenedorparte2 {
  position: relative;
  width: 120px;
  height: 480px;
  margin-top: 14px;
  margin-bottom: -18px;
  margin-left: 45px;

  display: grid;
  grid-template-rows: 10%, 40%, 50%;
}

.cont2_1 {
  width: 320px;
  height: 40px;
  border: 1px solid #dfd9d9;
  color: rgb(0, 0, 0);
  display: grid;
  grid-template-columns: 1fr 1fr;
  background-color: rgba(224, 217, 217, 0.363);
}

.cont2_2 {
  display: grid;
  grid-template-rows: 60% 15% 25%;
}

.cara1 img {
  margin-top: -10px;
  width: 40%;
  height: auto;
  object-fit: contain;
}


/* ooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo */

.cara2,
.cara3 {
  font-size: 1rem;
  margin-left: 0%;
  color: rgb(49, 49, 49);
  border: 1px solid #dfd9d9;
  display: grid;
  grid-template-columns: 30% 70%;
  background-color: rgba(224, 217, 217, 0.363);
}

.nom {
  width: 160px;
  height: 40px;
  border: 1px solid #dfd9d9;
}

.nom h1 {

  text-align: left;
  font-size: 0.9rem;
  margin-left: 25%;
  color: rgb(49, 49, 49);
}

.num {
  width: 157px;
  height: 40px;
  border: 1px solid #dfd9d9;

}

.num h1 {
  text-align: left;
  font-size: 1rem;
  margin-left: 40%;
  color: rgb(49, 49, 49);
}

.cont2_2 {
  position: relative;
  width: 320px;
  height: 200px;
  border: 1px solid #dfd9d9;
  color: rgb(0, 0, 0);
  background-color: rgba(224, 217, 217, 0.363);
}

.cara1mitad {
  position: relative;
  width: 340px;
  height: 200px;
  margin-left: 18px;
 
  color: rgb(0, 0, 0);  
  border: 1px solid #dfd9d9;
  background-color: rgba(224, 217, 217, 0.363);
}


.cont2_3 {
  position: relative;
  width: 320px;
  height: 220px;
  border: 1px solid #dfd9d9;
  color: rgb(0, 0, 0);
  display: grid;
  grid-template-columns: 1fr 1fr;
}

.parte1 {
  position: relative;
  width: 400px;
  height: 65px;
  background-color: rgba(232, 51, 42, 0.8);
  border: 1px solid #dfd9d9;
  color: rgb(0, 0, 0);
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;

}

.parte2 {
  position: relative;
  width: 400px;
  height: 500px;
  border: 1px solid #dfd9d9;
  background-color: rgba(169, 169, 169, 0.7);
  color: black;
  border-bottom-left-radius: 15px;
  border-bottom-right-radius: 15px;
}

.partemitad {
  position: relative;
  width: 400px;
  height: 500px;
  border: 1px solid #dfd9d9;
  background-color: rgba(169, 169, 169, 0.7);
  color: black;
  border-bottom-left-radius: 15px;
  border-bottom-right-radius: 15px;
}

.partemitad {
  display: grid;
  grid-template-rows: 10% 45% 45%;
}

.partemitad_2 {
  position: relative;
  width: 390px; 
  height: 220px;
  margin-top: -8px;
  margin-left: 4px; 
  border: 1px solid #dfd9d9; 
  background-color: rgba(224, 217, 217, 0.363);
  overflow-y: auto; 
}

.partemitad_2 {
    --sb-track-color: #d4cfcf;
    --sb-thumb-color: #e0dbdb;
    --sb-size: 7px;
  
    
    
  }
  
  .partemitad_2::-webkit-scrollbar {
    width: var(--sb-size);
  }
  
  .partemitad_2::-webkit-scrollbar-track {
    background: var(--sb-track-color);
    border-radius: 3px;
  }
  
  .partemitad_2::-webkit-scrollbar-thumb {
    background: var(--sb-thumb-color);
    border-radius: 3px;
  }
.contenedor3parte1 {
  position: relative;
  width: 400px;
  height: 565px;
  border: 1px solid #dfd9d9;
  background-color: rgba(169, 169, 169, 0.7);
  color: black;
  border-bottom-left-radius: 15px;
  border-bottom-right-radius: 15px;
}

#pide2 {
  margin-left: 4px;
  width: 150px;
  height: 30px;
  border: 1px solid rgb(216, 212, 212);
  background-color: aliceblue;
  color: black;
}

#pide2::placeholder {
  text-indent: 4px;
}

#pide1,
#pide2 {
  margin-top: 25px;
}

.column1 {
  display: grid;
  grid-template-rows: 1fr 1fr 1fr 1fr 1fr 1fr 1fr;

}

.column2 {
  display: grid;
  grid-template-rows: 1fr 1fr 1fr 1fr 1fr 1fr 1fr;

}
.partemitad_3{
  display: grid;
  grid-template-rows: 3fr 1fr;
}

.fila1,
.fila2,
.fila3,
.fila4,
.fila5,
.fila6,
.fila7,
.fila8,
.fila9,
.fila10,
.fila11,
.fila12,
.fila13,
.fila14 {
  font-size: 1rem;
  margin-left: 0%;
  color: rgb(49, 49, 49);
  border: 1px solid #dfd9d9;
  background-color: rgba(224, 217, 217, 0.363);
}
.img_ganador h1{
  font-size: 1rem;
  margin-left: 0%;
  margin-top: -2px;
  color: rgb(49, 49, 49);
}
#fotoo{
  margin-top: 8px;
  width: 30%;
  height: auto;
  object-fit: contain;
}

#results {
  margin-top: 14px;
}

.round-result {
  position: relative;
  width: 366px;
  margin-left: 7px;
  margin-bottom: 2px;
  padding: 1px;
  border: 1px solid #dfd9d9;
  background-color: rgba(224, 217, 217, 0.363);
}



@media (max-width: 900px) {
  .contenedor {
    position: relative;
    width: 350px;
    height: 300px;
    margin-top: -200px;
    margin-bottom: -18px;
    margin-left: -50px;
    display: grid;
    grid-template-rows: 4fr, 1fr;

  }

  body {
    height: 100%;
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    background-image: none;
    background-size: 100%;
    background-position: center;
    background-repeat: no-repeat;
  }

}
</style>
