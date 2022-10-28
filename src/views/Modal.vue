<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Modal</ion-title>
        <ion-buttons slot="end">
          <ion-button @click="dismiss()">
            Dismiss
          </ion-button>
        </ion-buttons>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true" class="ion-padding">
      <h1>Test modal</h1>
      <p>Opening this modal makes the statusbar style go back to system (light) for as long as the app is running.</p>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButton, modalController, IonButtons } from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'TestModal',
  props: {
    setCanDismiss: {
      type: Function,
    }
  },
  setup: (props) => {
    
    async function dismiss() {
      if(props.setCanDismiss) {
        props.setCanDismiss(true);
      }
      modalController.dismiss();
    }
    
    return {
      dismiss,
    };
  },
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonButton,
    IonButtons,
  }
});
</script>

<style scoped>

</style>
