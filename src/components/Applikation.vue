<template>
  <div class="applikation-container">
    <h1>Jeg er en h1</h1>
    <h2>Jeg er en h2</h2>
    <h3>Jeg er en h3</h3>
    <h4>Jeg er en h4</h4>
    <h5>Jeg er en h5</h5>
    {{currentTime}}
    <hr>
    Dynamisk komponent:
    <dynamic-component text="Jeg er en dynamisk komponent"></dynamic-component>
    <hr>
    <a href="http://www.google.com" target="_blank">Link til Google</a>
    <div class="spinner" v-if="loadingResponse" aria-label="Henter indhold" />
    {{response}}
    <hr>
    <button class="button">Jeg er en knap</button>
    <hr>
    <div class="row">
      <div class="col-md-6 col-xs-12 align-self-baseline">
        <h1>Applikationer</h1>
        <p>
          Med applikationer forstås den software, der reelt driver jeres virksomhed. Derfor er applikationerne ofte dér, hvor hackere søger hen, når
          de søger efter informationer eller skal finde en indgang til at sprede ondsindede aktiviteter.
        </p>
        <p>
          Nogle hackere deler også websider, dokumentfiler og andet indhold fra egne hjemmesider eller andre troværdige kilder. Og når umistænksomme
          ofre besøger indholdet med en ikke-sikret browser eller andet software, lukker de dermed hackeren ind på deres enhed og i sidste ende ind
          i virksomheden.
        </p>
        <p>I det følgende er der to generelle spørgsmål til applikationer, og herefter risikovurderer du jeres individuelle systemer.</p>
      </div>
      <div class="col-md-6 col-xs-12 align-self-baseline">
        <h2>Sådan gør du</h2>
        <p>Du skal vurdere sandsynlighed og konsekvens på to forskellige skalaer, som hver har fem svarmuligheder. Skalaerne ser ud som følger.</p>
        <div class="accordion-wrapper">
          <ul class="accordion accordion-multiselectable">
            <li>
              <button class="accordion-button" aria-expanded="false" aria-controls="a1">Skala for sansynlighed</button>
              <div id="a1" aria-hidden="true" class="accordion-content">
                <p>
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
                  enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
                </p>
              </div>
            </li>
            <li>
              <button class="accordion-button" aria-expanded="false" aria-controls="a2">Skala for konsekvens</button>
              <div id="a2" aria-hidden="true" class="accordion-content">
                <p>
                  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
                  enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
                </p>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
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

var dynamicComponent = {
  template: '<div>{{text}}</div>',
  props: ['text'],
};

@Component({
  name: 'Applikation',
  components: {
    dynamicComponent
  }
})
export default class Applikation extends Vue {
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

</style>
