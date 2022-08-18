<template>
  <q-layout view="lHh Lpr lFf" class="bck">
    <q-header elevated>
      <q-bar class="bg-black">
          <q-btn dense flat round icon="lens" size="8.5px" color="red" />
          <q-btn dense flat round icon="lens" size="8.5px" color="yellow" />
          <q-btn dense flat round icon="lens" size="8.5px" color="green" />
          <div class="col text-center text-weight-bold">
            Viewer
          </div>
      </q-bar>
    </q-header>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import EssentialLink from 'components/EssentialLink.vue'


import { Vue, Component } from 'vue-property-decorator';

@Component({
  components: { EssentialLink }
})
export default class MainLayout extends Vue {
  leftDrawerOpen = false;
}
</script>

<style lang="scss" scoped>
  .bck{
    background-color: #242424;
    color: white;
  }
</style>
