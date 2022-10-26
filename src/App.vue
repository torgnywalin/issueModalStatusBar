<template>
  <ion-app>
    <ion-router-outlet id="main" />
  </ion-app>
</template>

<script lang="ts">
import { IonApp, IonRouterOutlet } from '@ionic/vue';
import { defineComponent } from 'vue';
import { StatusBar, Style } from '@capacitor/status-bar';

export default defineComponent({
  name: 'App',
  setup: () => {
    StatusBar.setStyle({ style: Style.Dark })
  },
  components: {
    IonApp,
    IonRouterOutlet
  }
});
</script>