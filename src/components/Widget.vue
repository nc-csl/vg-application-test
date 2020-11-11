<template>
  <div class="widget-container">
    <h1>ERST widget</h1>
    {{currentTime}}
    <hr>
    <a href="http://www.google.com" target="_blank">Link til Google</a>
    <div class="spinner" v-if="loadingResponse" aria-label="Henter indhold" />
    {{response}}
    <hr>
    <div class="card">
      <div class="card-header">
        <h3 class="header-title">Eksempel på card-komponenten</h3>
      </div>
      <div class="card-text">
        <p>Du kan bruge cards til at gruppere funktionalitet, der adskiller
          sig fra sidens øvrige indhold. Cards kan placeres i et <a
            href="#">grid</a>, således at de står side om
          side.</p>
      </div>

      <div class="card-footer card-action">

        <div class="action-links">
          <a href="#">Gå til komponent</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import axios from 'axios';
import { DateTime } from 'luxon';

@Component({
  name: 'Widget'
})
export default class Widget extends Vue {
  private currentTime = '';
  private response = {};
  private error = {};
  private loadingResponse = false;

  mounted() {
    this.currentTime = DateTime.local().toISO();
    this.loadingResponse = true;
    this.callExternalApi();
  }

  private async callExternalApi() {
    axios.get('https://httpbin.org/get').then((rsp: any) => {
      this.response = rsp;
      this.loadingResponse = false;
    }).catch((error: any) => {
      this.error = error;
    });
  }
}
</script>
<style lang="scss" scoped>
  h1 {
    color: $color-link;
  }
</style>
