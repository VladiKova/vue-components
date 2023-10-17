<script setup>
import { ref, onMounted } from 'vue';

const message = "Esto es una prueba";
const styleColor = "color:purple";

const iconosAlimentos = ["🍔", "🍕", "🍟", "🌭", "🍦", "🍩", "🍪",
  "🍰", "🍫", "🍭", "🍯", "🍤", "🥪", "🥙", "🍣", "🍥"];
const arrayDeObjetos = [
  { nombre: "Manzana", color: "Rojo", precio: 1.0, cantidad: 10 },
  { nombre: "Banana", color: "Amarillo", precio: 0.5, cantidad: 20 },
  { nombre: "Naranja", color: "Naranja", precio: 0.75, cantidad: 15 },
  { nombre: "Fresa", color: "Rojo", precio: 1.2, cantidad: 12 },
];

const handleEvent = () => {
  let li = document.getElementsByTagName("li");
  for (let element of li) {
    element.className = "li-color";
  }
}

let activo = ref(true);
const showList = () => {
  activo.value = !activo.value; // Cambiar el valor de activo al hacer clic
  buttonDes.value = activo.value ? "Ocultar lista" : "Mostrar lista"; // Cambiar el texto del botón
}
const buttonDes = ref("Mostrar lista");

onMounted(() => {
  setTimeout(() => {
    document.getElementsByTagName("h1")[0].style = styleColor;

  }, 4000);
});
</script>

<template>
  <h1>Hola vue.js {{ message.toUpperCase() }}</h1>
  <h2 :class="{ 'inactive': !activo }">{{ activo ? "Estoy activo" : "Estoy inactivo" }}</h2>
  <h3 v-if="activo">Nuevo activo</h3>
  <h3 v-else> No activo</h3>
  <div :class="'container'">
    <div>
      <ul>
        <span>Lista de iconos</span>
        <li v-for="(alimento, index) in iconosAlimentos.slice(0, 4)" :key="index">
          {{ index + 1 }}-{{ alimento }}
        </li>
      </ul>
      <button @click.middle="handleEvent"> Cambiar color</button>
    </div>
    <div>
      <ul v-show="(activo)">
        <span>Lista de comida</span>
        <li v-for="(alimento, index) in arrayDeObjetos" :key="alimento.nombre">
          {{ index + 1 }}-{{ alimento.nombre }}
          <ul>
            <template v-for="(value, key) in alimento" :key="`${key}-${index}`">
              <li v-if="key != 'nombre'">
                {{ key }}: {{ value }}
              </li>
            </template>
          </ul>
        </li>
      </ul>
      <button @click="showList">
        {{ buttonDes }}
      </button>
    </div>
  </div>
</template>

<style>
h1 {
  color: red;
}

.inactive {
  color: green;
}

.container {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: row;
  flex-grow: 1;

}

.container>div {
  text-align: left;
  padding: 1%;
  border: 1px solid white;
  width: 100%;
}

ul {
  list-style-type: none;
}

.li-color {
  color: cyan;
}
</style>