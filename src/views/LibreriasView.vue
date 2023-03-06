<template>
    <div>
      <navigation/>
      <h1>Librerias Registradas</h1>
      <v-data-table
        :headers="headers"
        :items="librerias"
        class="elevation-2"
      ></v-data-table>
    </div>
  </template>
  <script>
  export default {
    data () {
      return {
        headers: [
          { text: 'Id Libreria', value: 'libreriaId' },
          { text: 'Nombre', value: 'nombre' },
          { text: 'Correo de Contacto', value: 'correoContacto' },
          { text: 'Dirección', value: 'direccion' },
          { text: 'Telefono', value: 'telefono' },
          { text: 'GUID', value: 'libreriaGuid' },
        ],
        librerias: [],
        search: '',
        pagination: {},
        selected: []
      }
    },
    created () {
      this.mostrarLibrerias()
    },
    methods: {
      mostrarLibrerias () {
        fetch('https://localhost:44327/api/Librerias')
          .then((response) => response.json())
          .then((data) => (this.librerias = data))
      }
    }
  }
  </script>