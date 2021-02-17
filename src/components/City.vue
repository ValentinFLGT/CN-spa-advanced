<template>
  <div>
    <h2>{{ name }}</h2>
    <p>Temps : {{ weather }} - Température : {{ temperature }}°C</p>
    <p><em>Dernière mise à jour : {{ formattedDate }}</em></p>
  </div>
</template>

<script lang="ts">
import {Prop} from 'vue-property-decorator';
import {format} from "timeago.js";

export default class City {

  constructor(name: string, weather: string, temperature: number, updatedAt: Date) {
    this.name = name
    this.weather = weather
    this.temperature = temperature
    this.updatedAt = updatedAt
  }

  @Prop() private name: string;
  @Prop() private weather: string;
  @Prop() private temperature: number;
  @Prop() private readonly updatedAt: Date;

  get formattedDate(): string {
    return format(this.updatedAt, 'fr')
  }
}
</script>

<style scoped>
h1 {
  margin: 40px 0 0;
}
</style>
