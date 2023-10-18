<template>
  <ion-header>
    <ion-toolbar>
      <ion-buttons slot="end">
        <ion-button @click="cancel()">Cancel</ion-button>
      </ion-buttons>
    </ion-toolbar>
  </ion-header>
  <ion-content class="ion-padding">
    <ion-item>
      <p>Modal 2: {{ content }}</p>
    </ion-item>
    <ion-item>
      <ion-button @click="confirmOnWillDismiss()">Confirm using "onWillDismiss" with data (bug?)</ion-button>
    </ion-item>
    <ion-item>
      <ion-button @click="confirmOnDidDismiss()">Confirm using "onDidDismiss" with data (okay)</ion-button>
    </ion-item>
    <ion-item>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Mollitia unde accusamus ad sunt nemo
        nostrum
        enim temporibus voluptate quos consectetur expedita officiis, dolorum tempora in tempore sapiente
        ullam at
        hic.</p>
    </ion-item>
  </ion-content>
</template>
  
<script setup lang="ts">
import { IonButton, IonButtons, IonContent, IonHeader, IonItem, IonToolbar, modalController } from '@ionic/vue';
import { ref } from 'vue';

const content = ref('Hello from modal 2!');

const cancel = () => modalController.dismiss(null, 'cancel');

const confirmOnWillDismiss = () => modalController.dismiss(content.value, 'confirmOnWillDismiss');
const confirmOnDidDismiss = () => modalController.dismiss(content.value, 'confirmOnDidDismiss');
</script>
