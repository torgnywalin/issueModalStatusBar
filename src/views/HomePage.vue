<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Blank</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true" class="ion-padding">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Home</ion-title>
        </ion-toolbar>
      </ion-header>
      <p>StatusBar is set to 'DARK' with StatusBar.setStyle({ style: Style.Dark }) in App.vue</p>
    
      <div id="container">
        <ion-button @click="openModal(true)">Open Card modal (With swipeToClose: true)</ion-button>
        <ion-button @click="openModal(false)">Open Card modal (With swipeToClose: false)</ion-button>
        <ion-button @click="setDarkMode()">Reset statusbar</ion-button>
        <br/>
        <br/>
        <em>Style is now: {{ style }}</em>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButton, modalController, onIonViewWillEnter } from '@ionic/vue';
import { defineComponent, ref } from 'vue';
import TestModal from './Modal.vue'
import { StatusBar, Style } from '@capacitor/status-bar';

export default defineComponent({
  name: 'HomePage',
  setup: () => {
    const style: any = ref(null);

    getStatusBarStyle();

    async function getStatusBarStyle() {
      const info = await StatusBar.getInfo();
      style.value = info.style;
      //alert(`Style is now: ${style.value}`);
    }

    async function openModal(swipeToClose: boolean) {
      const main = document.getElementById('main');
      const modal = await modalController.create({
        component: TestModal,
        presentingElement: main || undefined,
        swipeToClose: swipeToClose,
      });
      await modal.present();
      await modal.onDidDismiss();
      getStatusBarStyle();
    }

    async function setDarkMode() {
      StatusBar.setStyle({ style: Style.Dark });
      getStatusBarStyle();
    }

    return {
      openModal,
      setDarkMode,
      style,
    };
  },
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonButton,
  }
});
</script>

<style scoped>

</style>
