<template>
  <ion-page
    ><ion-header>
      <ion-toolbar>
        <ion-title>Home Page</ion-title>
        <ion-buttons slot="end">
          <ion-button>LOGOUT</ion-button>
        </ion-buttons>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <h1>Home Page</h1>
      <p>This is the Home Page</p>
      <ion-button @click="ionRouter.push('/next')" color="danger">
        Next Page</ion-button
      >
      <ion-button @click="takePicture"> Camera</ion-button>
      <ion-img :src="imageURL"></ion-img>
    </ion-content>
  </ion-page>
</template>
<script lang="ts" setup>
import { ref } from 'vue';
import { Camera, CameraResultType } from '@capacitor/camera';

const ionRouter = useIonRouter();
const imageURL = ref(null);
definePageMeta({
  alias: ['/', '/home'],
});

const takePicture = async () => {
  const image = await Camera.getPhoto({
    quality: 90,
    allowEditing: true,
    resultType: CameraResultType.Uri,
  });

  // image.webPath will contain a path that can be set as an image src.
  // You can access the original file using image.path, which can be
  // passed to the Filesystem API to read the raw data of the image,
  // if desired (or pass resultType: CameraResultType.Base64 to getPhoto)
  imageURL.value = image.webPath;

  // Can be set to the src of an image now
};
</script>
