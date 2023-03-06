<template>
    <div>
      <div>
      <navigation/>
      <h1>Busqueda de Librerias por GUID</h1>
    </div>
        <v-col cols="12" md="4">
            <v-text-field
            v-model="libreriaGuid"
            label="Escribe el Guid de la Libreria"
            outlined
            required></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
            <v-btn block outlined depressed @click="Buscar" color="success"> Buscar </v-btn>
        </v-col>
      <v-data-table
        v-if="record"
        :headers="headers"
        :items="record"
        :items-per-page="5"
      ></v-data-table>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        libreriaGuid: "",
        record: null,
        headers: [
          { text: 'Id Libreria', value: 'libreriaId' },
          { text: 'Nombre', value: 'nombre' },
          { text: 'Correo de Contacto', value: 'correoContacto' },
          { text: 'Dirección', value: 'direccion' },
          { text: 'Telefono', value: 'telefono' },
          { text: 'GUID', value: 'libreriaGuid' },
        ]
      };
    },
    methods: {
      async Buscar() {
        const response = await fetch(`https://localhost:44327/api/Librerias/${this.libreriaGuid}`);
        if (!response.ok) {
          this.record = null;
          alert('GUID Incorrecta')
          return;
        }
        const data = await response.json();
        this.record = [data];
      }
    }
  };
  </script>