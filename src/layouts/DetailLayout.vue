<template>
  <q-layout view="lHh Lpr lFf">
    <q-page-container class="bg-Result">
      <q-toolbar class="bar text-white">
        <q-btn flat round dense icon="menu" class="q-mr-sm" />

        <q-toolbar-title>
          <img src="~assets/ngmusic_2022-08-13/ngmusic.png" class="ngmusic"
        /></q-toolbar-title>
        <q-btn flat round dense icon="search" @click="winSearch" />
      </q-toolbar>
      <router-view />

      <q-dialog v-model="isOpen" persistent full-width :maximized="true">
        <q-card class="bgwhite text-white">
          <q-card-section class="row items-center q-pb-none">
            <q-space />
            <q-btn icon="close" flat round dense v-close-popup />
          </q-card-section>
          <q-card-section>
            <index-page
              :logo="false"
              class="q-ml-xl"
              ref="indexpage"
              @onSearch="onSearchs"
            />
          </q-card-section>
        </q-card>
      </q-dialog>
    </q-page-container>
  </q-layout>
</template>


<script>
import IndexPage from "../pages/IndexPage.vue";
export default {
  components: {
    IndexPage,
  },
  data() {
    return {
      isOpen: false,
    };
  },
  methods: {
    winSearch() {
      this.isOpen = true;
    },
    async onSearchs() {
      this.isOpen = false;
      this.$refs.indexpage.onSearch();
    },
  },
};
</script>
