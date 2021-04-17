<template>
  <div class="container-fluid text-center">
    <!--Encabezado-->
    <div class="encabezado col-12 mt-5 mb-3">
      <h1>Random Gif Cat</h1>
    </div>
    <!--Formulario-->
    <div class="formulario row">
      <!--Formulario - Labels-->
      <div class="label col-5">
        <div><label class="form-label d-flex justify-content-end">Título:</label></div>
        <div><label class="form-label d-flex justify-content-end">Filtro:</label></div>
        <div><label class="form-label d-flex justify-content-end">Color:</label></div>
        <div><label class="form-label d-flex justify-content-end">Tamaño:</label></div>
      </div>
      <!--Formulario - Inputs-->
      <div class="col-3">
        <!-- ****** -->
        <div>
          <input type="text" class="form-control form-control-sm my-2" v-model="titulo">
        </div>
        <!-- ****** -->
        <div>
          <select class="form-select form-select-sm my-2" v-model="filtro">
            <option v-for="val in arrFiltros" :key="val">{{val}}</option>
          </select>
        </div>
        <!-- ****** -->
        <div>
          <select class="form-select form-select-sm my-2" v-model="color">
            <option v-for="val in arrColores" :key="val">{{val}}</option>
          </select>
        </div>
        <!-- ****** -->
        <div>
          <input type="text" class="form-control form-control-sm my-2" v-model="tamano">
        </div>
      </div>
      <!--Formulario - Figura-->
      <div class="col-4">
        <div class="figura rounded-circle" :style="{backgroundColor: this.color}"></div>
      </div>
    </div>
    <!--Boton-->
    <div class="boton col-12">
      <button @click="obtenerData()" type="button" class="btn btn-light m-3">Obtener mi gatito</button>
    </div>
    <!--Resultado-->
    <div class="resultado col-12 mb-5">
      <img :src="dataApi && dataApi.config && dataApi.config.url" alt="">
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "App",
  data() {
    return {
      titulo: "",
      filtro: "",
      color: "",
      tamano: "",
      dataApi: "",
      arrFiltros: ["blur", "mono", "sepia", "negative", "paint", "pixel"],
      arrColores: ["green", "orange", "blue", "red", "black", "yellow"]
    }
  },
  methods: {
    async obtenerData() {
      const url = `https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.tamano}&type=or`;
      try {
        const request = await axios(url);
        if(!request) return;
        console.log(request);
        this.dataApi = request;
      } catch (error) {
        console.log(error);
      }
    }
  },
};
</script>

<style lang="scss">
  .formulario {
    background-color: lightcoral;
  }

  label {
    margin: .8rem 0;
  }

  .figura {
    width: 30px;
    height: 30px;
    background-color: white;
    margin-top: 5.5rem;
  }
</style>
