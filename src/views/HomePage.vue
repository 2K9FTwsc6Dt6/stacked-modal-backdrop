<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <div id="container">
        <h1>Backdrop remains partially visible and crops content after closing modal 2 (inline and controller).</h1>
        <p>Reproducible: Chrome 118 under Windows 10 (native) and macOS Sonoma (BrowserStack).<br>
          Not under Windows 10/11 in BrowserStack and an Ubuntu 23.10 VMware.<br>
          Safari and Firefox seem to be not affected.</p>
        <p><strong>Maximum window width: 767px</strong></p>
        <ion-item>
          <ion-button id="open-modal-1" expand="block">Open Modal 1 (Inline)</ion-button>
        </ion-item>
        <ion-item>
          <ion-button @click="openControllerModals" expand="block">Open Modal 1 (Controller)</ion-button>
        </ion-item>
        <ion-modal ref="modal1" trigger="open-modal-1" :initial-breakpoint="0.75" :breakpoints="[0, 0.75]">
          <ion-header>
            <ion-toolbar>
              <ion-buttons slot="end">
                <ion-button @click="cancel1()">Cancel</ion-button>
              </ion-buttons>
            </ion-toolbar>
          </ion-header>
          <ion-content class="ion-padding">
            <ion-item>
              <p>Modal 1: {{ content1 }}</p>
            </ion-item>
            <ion-item>
              <ion-button id="open-modal-2" expand="block">Open Modal 2</ion-button>
              <ion-modal ref="modal2" trigger="open-modal-2" :initial-breakpoint="0.5" :breakpoints="[0, 0.5]"
                @willDismiss="onWillDismiss2" @didDismiss="onDidDismiss2">
                <ion-header>
                  <ion-toolbar>
                    <ion-buttons slot="end">
                      <ion-button @click="cancel2()">Cancel</ion-button>
                    </ion-buttons>
                  </ion-toolbar>
                </ion-header>
                <ion-content class="ion-padding">
                  <ion-item>
                    <p>Modal 2: {{ content2 }}</p>
                  </ion-item>
                  <ion-item>
                    <ion-button color="danger" @click="confirmOnWillDismiss2()">Confirm using "onWillDismiss" with data
                      (bug)</ion-button>
                  </ion-item>
                  <ion-item>
                    <ion-button color="success" @click="confirmOnDidDismiss2()">Confirm using "onDidDismiss" with data
                      (okay)</ion-button>
                  </ion-item>
                  <ion-item>
                    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Mollitia unde accusamus ad sunt nemo
                      nostrum
                      enim temporibus voluptate quos consectetur expedita officiis, dolorum tempora in tempore sapiente
                      ullam at
                      hic.</p>
                  </ion-item>
                </ion-content>
              </ion-modal>
            </ion-item>
            <ion-item>
              <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Mollitia unde accusamus ad sunt nemo nostrum
                enim temporibus voluptate quos consectetur expedita officiis, dolorum tempora in tempore sapiente ullam at
                hic.</p>
            </ion-item>
          </ion-content>
        </ion-modal>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonButton, IonButtons, IonContent, IonHeader, IonItem, IonModal, IonPage, IonToolbar, modalController } from '@ionic/vue';
import { OverlayEventDetail } from '@ionic/core/components';
import { ref } from 'vue';
import ControllerModal1 from './ControllerModal1.vue';

const content1 = ref('Content 1');
const content2 = ref('Hello from modal 2!');

let count1 = 0;

const modal1 = ref();
const modal2 = ref();

const cancel1 = () => modal1.value.$el.dismiss(null, 'cancel');
const cancel2 = () => modal2.value.$el.dismiss(null, 'cancel');

const confirmOnWillDismiss2 = () => modalController.dismiss(content2.value, 'confirmOnWillDismiss');
const confirmOnDidDismiss2 = () => modalController.dismiss(content2.value, 'confirmOnDidDismiss');

const onWillDismiss2 = (event: CustomEvent<OverlayEventDetail>) => {
  if (event.detail.role === 'confirmOnWillDismiss') {
    content1.value = `${event.detail.data} ✖ ${++count1} (onWillDismiss)`;
  }
};

const onDidDismiss2 = (event: CustomEvent<OverlayEventDetail>) => {
  if (event.detail.role === 'confirmOnDidDismiss') {
    content1.value = `${event.detail.data} ✖ ${++count1} (onDidDismiss)`;
  }
};

// Controller modals version

const openControllerModals = async () => {
  const modal = await modalController.create({
    component: ControllerModal1,
    initialBreakpoint: 0.75,
    breakpoints: [0, 0.75]
  });

  await modal.present();
};
</script>

<style scoped>
#container {
  text-align: center;

  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;

  color: #8c8c8c;

  padding: 1rem;

  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
