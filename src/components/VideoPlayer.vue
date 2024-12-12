<template>
  <video id="demo-video" v-if="url" controls width="100%">
    <source :src="url" type="video/mp4" height="200" />
  </video>
</template>

<script>

// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
import { getStorage, ref, getDownloadURL } from "firebase/storage";

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: process.env.FIREBASE_API_KEY,
  authDomain: `${process.env.FIREBASE_PROJECT_ID}.firebaseapp.com`,
  projectId: process.env.FIREBASE_PROJECT_ID,
  storageBucket: `${process.env.FIREBASE_PROJECT_ID}.appspot.com`,
  messagingSenderId: "709267513332",
  appId: "1:709267513332:web:49d147bdbffab09ea6a3a1"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
const storage = getStorage(app);

export default {
  name: 'video-player',
  data: () => ({
    url: null
  }),
  async created () {
    this.url = await getDownloadURL(ref(storage, `gs://${process.env.FIREBASE_PROJECT_ID}.appspot.com/demo-workout.mp4`))
    console.log(this.url)
  }

}
</script>
