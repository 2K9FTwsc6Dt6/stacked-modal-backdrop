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
      <p>Modal 1: {{ content }}</p>
    </ion-item>
    <ion-item>
      <ion-button @click="openModal2()" expand="block">Open Modal 2</ion-button>
    </ion-item>
    <ion-item>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Mollitia unde accusamus ad sunt nemo nostrum
        enim temporibus voluptate quos consectetur expedita officiis, dolorum tempora in tempore sapiente ullam at
        hic.</p>
    </ion-item>
  </ion-content>
</template>
  
<script setup lang="ts">
import { IonButton, IonButtons, IonContent, IonHeader, IonItem, IonToolbar, modalController } from '@ionic/vue';
import { ref } from 'vue';
import ControllerModal2 from './ControllerModal2.vue';

const content = ref('Content 1');

const cancel = () => modalController.dismiss(null, 'cancel');

const openModal2 = async () => {
  const modal = await modalController.create({
    component: ControllerModal2,
    initialBreakpoint: 0.5,
    breakpoints: [0, 0.5]
  });

  await modal.present();

  const { data, role } = await modal.onWillDismiss();

  if (role === 'confirm') {
    content.value = data;
  }
};
</script>
