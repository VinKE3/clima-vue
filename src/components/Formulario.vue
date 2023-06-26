<script setup>
import { reactive, ref } from "vue";
import Alerta from "./Alerta.vue";
const paises = [
  { codigo: "US", nombre: "Estados Unidos" },
  { codigo: "MX", nombre: "México" },
  { codigo: "AR", nombre: "Argentina" },
  { codigo: "CO", nombre: "Colombia" },
  { codigo: "CR", nombre: "Costa Rica" },
  { codigo: "ES", nombre: "España" },
  { codigo: "PE", nombre: "Perú" },
];
const error = ref("");
const busqueda = reactive({
  ciudad: "",
  pais: "",
});
const emit = defineEmits(["obtener-clima"]);
const consultarClima = () => {
  if (busqueda.ciudad === "" || busqueda.pais === "") {
    error.value = "Todos los campos son obligatorios";
    return;
  }
  emit("obtener-clima", busqueda);
  error.value = "";
};
</script>
<template>
  <form class="formulario" @submit.prevent="consultarClima">
    <Alerta v-if="error">{{ error }}</Alerta>
    <div class="campo">
      <label for="ciudad">Ciudad</label>
      <input
        type="text"
        id="ciudad"
        placeholder="Ciudad"
        v-model="busqueda.ciudad"
      />
    </div>
    <div class="campo">
      <label for="pais">Pais</label>
      <select id="pais" v-model="busqueda.pais">
        <option value="">-- Seleccione un pais --</option>
        <option v-for="pais in paises" :key="pais.codigo" :value="pais.codigo">
          {{ pais.nombre }}
        </option>
      </select>
    </div>
    <input type="submit" value="Buscar Clima" />
  </form>
</template>

<style lang="scss" scoped></style>
