<template>
  <ion-card>
    <ion-card-header>
      <ion-card-title>Camera</ion-card-title>
    </ion-card-header>

    <ion-card-content>
      <ion-button expand="block" @click="takePicture">
        <ion-icon slot="start" :icon="cameraIcon" /> Take Picture
      </ion-button>

      <ion-text v-if="errorMessage" color="danger">
        <p>{{ errorMessage }}</p>
      </ion-text>
    </ion-card-content>
  </ion-card>
</template>

<script setup lang="ts">
import {
  IonButton,
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardTitle,
  IonIcon,
  IonText,
} from "@ionic/vue";
import { camera as cameraIcon } from "ionicons/icons";
import { Camera, CameraResultType, CameraSource } from "@capacitor/camera";
import { ref } from "vue";

const errorMessage = ref("");

const emit = defineEmits<{
  (event: "photoCaptured", photo: string): void;
}>();

const takePicture = async () => {
  try {
    errorMessage.value = "";
    const image = await Camera.getPhoto({
      quality: 90,
      allowEditing: false,
      resultType: CameraResultType.Uri,
      source: CameraSource.Camera,
    });

    if (image.webPath) {
      emit("photoCaptured", image.webPath);
    }
  } catch (error: any) {
    // Handling kapag kinancel ng user ang pagkuha ng litrato
    if (error?.message !== "User cancelled photos app") {
      errorMessage.value = "Failed to take photo. Please try again.";
    }
  }
};
</script>