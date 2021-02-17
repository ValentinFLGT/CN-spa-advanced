<template>
  <div>
    <br/>
    <p>{{ quote }}</p>
    <button @click="refreshQuote()">Nouvelle citation</button>
    <div v-if="loading" style="color: orange;">Chargement en cours...</div>
    <div v-if="success" style="color: green;">Le chargement est terminé.</div>
    <div v-if="error" style="color: red;">{{ error }}</div>
  </div>
</template>

<script lang="ts">
import axios from 'axios';

export default class EasterEgg {

  loading: boolean = false
  success: boolean = false
  error: string = ""
  quote: string = ""

  refreshQuote() {
    console.log('created');
    this.loading = true;
    axios.get('https://kaamelott.hotentic.com/api/random').then((resp) => {
      this.quote = resp.data.citation.citation;
      this.loading = false;
    });
  }

  created() {
    this.refreshQuote();
  }

}
</script>
