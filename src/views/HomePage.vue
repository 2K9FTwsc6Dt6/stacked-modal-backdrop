<template>
  <ion-page>
  
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Blank</ion-title>
        </ion-toolbar>
      </ion-header>

      <div id="container">
        <ion-button id="open-modal-1" expand="block">Open Modal 1</ion-button>
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
              <p>Modal 1 content: {{ modifiedContent }}</p>
            </ion-item>
            <ion-item>
              <ion-button id="open-modal-2" expand="block">Open Modal 2</ion-button>
              <ion-modal ref="modal2" trigger="open-modal-2" :initial-breakpoint="0.5" :breakpoints="[0, 0.5]">
                <ion-header>
                  <ion-toolbar>
                    <ion-buttons slot="end">
                      <ion-button @click="cancel2()">Cancel</ion-button>
                    </ion-buttons>
                  </ion-toolbar>
                </ion-header>
                <ion-content class="ion-padding">
                  <ion-item>
                    <ion-button @click="++modifiedContent">Modify modal 1 content</ion-button>
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
import { IonButton, IonButtons, IonContent, IonHeader, IonItem, IonModal, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { ref } from 'vue';

const modifiedContent = ref(0);

const modal1 = ref();
const modal2 = ref();

const cancel1 = () => modal1.value.$el.dismiss(null, 'cancel');
const cancel2 = () => modal2.value.$el.dismiss(null, 'cancel');
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

  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
