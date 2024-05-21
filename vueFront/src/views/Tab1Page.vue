<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 1</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true" class="ion-padding">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Carro</ion-title>
        </ion-toolbar>
      </ion-header>

      <br>

      <ion-item v-for="carro in carros">
        <CardComponent imgclass="card-img" :titulo-card="carro.id" src="../../card.png" :subtitulo-card="carro.marca"
          :extra-content-card="carro.modelo" acolor="primary" bcolor="danger" adisable="false" bdisable="false"
          afill="solid" value-a="Editar" @actualizarDato="" @borrarDatoFisico="" bfill="solid" value-b="Eliminar"
          @agregar-dato="" value-c="Agregar carro" id-c="abrir-modal" name-c="abrir-modal" ccolor="success" cdisable="false" cfill="solid">

        </CardComponent>

      </ion-item>


      <ion-modal trigger="abrir-modal" ref="modal">
        <ion-header>
          <ion-toolbar color="light">
            <ion-buttons slot="start">
              <ion-button @click="dismiss()">
                < Regresar</ion-button>
            </ion-buttons>
          </ion-toolbar>
        </ion-header>
        <div class="modal-content">
          <div id="data-form">
            <h1 class="ion-text-center">Editar Carro</h1>
            <ion-item color="light">
              <ion-input v-model="carro.marca" id="marca" type="text" label="Marca"
                placeholder="Digite el nombre del carro" required label-placement="floating"></ion-input>
            </ion-item>

            <ion-item color="light">
              <ion-input v-model="carro.modelo" id="marca" type="text" label="Modelo"
                placeholder="Digite la marca del carro" required label-placement="floating"></ion-input>
            </ion-item>

            <ion-item color="light">
              <ion-input v-model="carro.placa" id="placa" type="number" label="Placa"
                placeholder="Digite la placa del carro" required label-placement="floating"></ion-input>
            </ion-item>


            <ion-item color="light">
              <ion-input v-model="carro.color" id="caracteristicas" type="text" label="Características"
                placeholder="Digite las características..." required label-placement="floating"></ion-input>
            </ion-item>

            <ion-item color="light">
              <ion-input v-model="carro.usuario_id" id="referencia" type="text" label="Referencia"
                placeholder="Digite la referencia..." required label-placement="floating"></ion-input>
            </ion-item>
            <ion-item color="light">
              <ion-select interface="popover" label="Categoria" v-model="carro.categoriaId.id" placeholder="Seleccionar"
                cancelText="Volver" okText="Elegir">
                <ion-select-option v-for="categoria in categorias" :key="categoria.id" :value="categoria.id">{{
                  categoria.nombre }}</ion-select-option>
              </ion-select>
            </ion-item>
            <br>
            <ButtonComponent id="actualizar" icono="fa-solid fa-floppy-disk" value="ok" color="primary"
              @Click="actualizarCarro()" />
          </div>
        </div>
      </ion-modal>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonItem, IonModal, IonButton, IonSelect, IonSelectOption, IonText,IonInput, IonButtons } from '@ionic/vue';
import CardComponent from '@/components/CardComponent.vue';
import axios from 'axios';
import { onMounted, ref } from 'vue';
import ButtonComponent from '../components/ButtonComponent.vue';

let baseURL = 'http://localhost:9000/parcial/api/carro';

let carros = ref([{ }]);

let categorias = ref ([]);

let carro = {
  "id": 0,
    "marca": "",
      "modelo": "",
        "placa": "",
          "color": "",
            "categoriaId": {
    "id": 0,
      },
  "usuario_id": {
    "id": 0,
        }
};


function actualizarCarro(){};

async function findAllCars() {
  axios.get(baseURL)
    .then(response => {
      carros.value = response.data; 
      console.log(carros)
    })
    .catch(error => {
      console.error("¡Hubo un error!", error);
    });
}

const modal = ref()

const dismiss = () => {
  modal.value.$el.dismiss()


}; 

onMounted(async () => {
  await findAllCars();
});
</script>
