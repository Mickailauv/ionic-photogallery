<template>
  <div v-if="photos.length === 0" class="empty-gallery">
    <p>No photos yet.</p>
  </div>

  <ion-grid v-else>
    <ion-row>
      <ion-col
        v-for="(photo, index) in photos"
        :key="index"
        size="6"
        size-md="4"
      >
        <ion-img :src="photo" />
      </ion-col>
    </ion-row>
  </ion-grid>
</template>

<script setup lang="ts">
import {
  IonGrid,
  IonRow,
  IonCol,
  IonImg,
} from "@ionic/vue";

defineProps<{
  photos: string[];
}>();
</script>

<style scoped>
.empty-gallery {
  text-align: center;
  padding: 30px;
  color: #777;
}
</style>