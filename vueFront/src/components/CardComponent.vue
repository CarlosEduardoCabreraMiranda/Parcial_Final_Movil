<template>
    <ion-card v-bind="$attrs" id="large" class="ion-padding">
        <div :class="class">

            <ion-card-header>

                <ion-card-title id="cardtitle">{{tituloCard}}</ion-card-title>
                <h2 id="cardtext">{{ subtituloCard }}</h2>
                <h2 id="cardtext">{{ extraContentCard }}</h2>
            </ion-card-header>
            <ion-card-content>
                <ButtonComponent :id="idC" :fill="cfill" :color="ccolor" :disabled="cdisable" id="cBtn" :hidden="ahidden"
                    :name="nameC" :value="valueC" expand="full" nameMethod="agregarDato" @click="handleClickSave" />

                <ButtonComponent :fill="afill" :color="acolor" :disabled="adisable" id="aBtn" :hidden="ahidden"
                    :name="nameA" :value="valueA" expand="full" nameMethod="actualizarDato"
                    @click="handleClickUpdate" />
                <ButtonComponent :fill="bfill" id="bBtn" :hidden="bhidden" :color="bcolor" :disabled="bdisable"
                    :name="nameB" :value="valueB" expand="full" nameMethod="borrarDatoFisico"
                    @click="handleClickDelete" />
            </ion-card-content>
        </div>
    </ion-card>
</template>

<script setup lang="ts">
import { IonCard, IonCardContent, IonCardHeader, IonCardSubtitle, IonCardTitle, IonImg  } from '@ionic/vue';
import {defineProps, defineEmits } from 'vue';
import ButtonComponent from './ButtonComponent.vue';




const props = defineProps({
    textAlt: String,
    tituloCard: String,
    class: String,
    subtituloCard: {
        type: String,
        default: "",
    },
    extraContentCard: {
        type: String,
        default: ""
    },
    nameA: String,
    nameB: String,
    nameC: String,
    valueA: {
        type: String,
        required: false,
        default: '',
    },
    valueB: {
        type: String,
        required: false,
        default: '',
    },
    valueC: {
        type: String,
        required: false,
        default: '',
    },
    ahidden: {
        type: String,
        default: 'true'
    },
    bhidden: {
        type: String,
        default: 'true'
    },
    acolor: {
        type: String,
        default: 'light'
    },
    bcolor: {
        type: String,
        default: 'light'
    },
    adisable: {
        type: String,
        default: 'true'
    },
    bdisable: {
        type: String,
        default: 'true'
    },
    afill: {
        type: String,
        default: 'outline'
    },
    bfill: {
        type: String,
        default: 'outline'
    },
    cdisable: {
        type: String,
        default: 'true'
    },
    cfill: {
        type: String,
        default: 'outline'
    },
    ccolor: {
        type: String,
        default: 'light'
    },
    idC: {
        type: String,
        required: false,
        default: '',
    },
});

const emit = defineEmits(['agregarDato' ,  'actualizarDato', 'borrarDatoFisico']);

// Métodos para manejar el clic en los botones
const handleClickSave = () => emit('agregarDato');
const handleClickUpdate = () => emit('actualizarDato');
const handleClickDelete = () => emit('borrarDatoFisico');
</script>

<style scoped src="../theme/container.css">
</style>