<template>
  <ion-page>
    <ion-tabs>
      <ion-router-outlet></ion-router-outlet>
      <ion-tab-bar slot="bottom">

        <ion-tab-button tab="uno" href="/tabs/uno">
          <ion-icon aria-hidden="true" :icon="medalOutline" />
          <ion-label>Notas</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="dos" href="/tabs/dos">
          <ion-icon aria-hidden="true" :icon="earthOutline" />
          <ion-label>Países</ion-label>
        </ion-tab-button>

      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script setup>
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage, IonRouterOutlet } from '@ionic/vue';
import { earthOutline, medalOutline } from 'ionicons/icons';
</script>
