<template>
  <div class="parent">
    <h1 class="title">Settings</h1>
    <hr>
    <div class="field">
      <b-switch v-model="fusionPositionEnabled" v-bind:disabled="geolocationDenied">Send position updates</b-switch>
      <p class="help">Use your location to help make Shuttle Tracker more accurate for everyone. Your location is gathered anonymously while Shuttle Tracker is open.</p>
    </div>
    <div class="field">
      <b-switch v-model="busButtonEnabled">Bus button</b-switch>
      <p class="help">Place a bus on other users' maps and let others place buses on your map.</p>
    </div>

    <router-link to="/about">About and privacy policy</router-link>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  computed: {
    busButtonEnabled: {
      get(): boolean {
        return this.$store.state.settings.busButtonEnabled;
      },
      set(value: boolean) {
        this.$store.commit('setSettingsBusButtonEnabled', value);
      },
    },
    fusionPositionEnabled: {
      get(): boolean {
        return this.$store.state.settings.fusionPositionEnabled && !this.$store.state.geolocationDenied;
      },
      set(value: boolean) {
        this.$store.commit('setSettingsFusionPositionEnabled', value);
      },
    },
    geolocationDenied: {
      get(): boolean {
        return this.$store.state.geolocationDenied;
      },
    },
  },
});
</script>

<style lang="scss" scoped>
.parent {
  padding: 20px;
}
</style>
