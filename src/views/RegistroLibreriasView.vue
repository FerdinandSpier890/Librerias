<template>
    <div>
      <div>
        <navigation />
        <h1>Registro de Librerias</h1>
      </div>
      <v-form v-model="valid">
        <v-container>
          <v-row>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="libreriaId"
                outlined
                label="Id de la Libreria"
                required
              ></v-text-field>
            </v-col>
            <br />
            <v-col cols="12" md="4">
              <v-text-field
                v-model="nombre"
                label="Nombre de la Libreria"
                outlined
                required
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="correoContacto"
                label="Correo de Contacto"
                outlined
                required
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="direccion"
                label="Dirección de la Libreria"
                outlined
                required
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                v-model="telefono"
                label="Telefono de la Libreria"
                outlined
                required
              ></v-text-field>
            </v-col>
            <br />
            <v-col cols="12" md="4">
              <v-btn depressed block outlined @click="Guardar" color="success">
                Registrar Libreria
              </v-btn>
            </v-col>
          </v-row>
          <div>
    <v-alert v-if="alertMessage" :value="true" type="success">
      {{ alertMessage }}
    </v-alert>
  </div>
        </v-container>
      </v-form>
    </div>
  </template>
  <script>
  import VueUUID from 'vue-uuid';
  export default {
    data: () => ({
      valid: false,
      libreriaId: "",
      nombre: "",
      correoContacto: "",
      direccion: "",
      telefono: "",
      libreriaGuid: VueUUID.v1(),
      alertMessage: null
    }),
    methods: {
      Guardar() {
        fetch("https://localhost:44327/api/Librerias", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            libreriaId: this.libreriaId,
            nombre: this.nombre,
            correoContacto: this.correoContacto,
            direccion: this.direccion,
            telefono: this.telefono,
            libreriaGuid: this.libreriaGuid
          }),
        })
          .then((res) => res.text())
          .then((data) => {
            this.$router.push("/lista");
            //this.alertMessage = 'Libreria Registrada Exitosamente';
            //this.alertMessage = true;
            alert("Libreria Registrada");
          });
      },
    },
  };
  </script>