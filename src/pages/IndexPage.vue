<template>
  <q-page class="flex flex-center">
    <div class="row bg_content">
      <div class="col-12">
        <img src="~assets/logo_2022-08-13/logo.png" class="logo" v-if="logo" />
      </div>

      <div class="col-12 q-ml-lg">
        <div
          class="text-white text-h6 text-center q-mb-lg"
          style="margin-left: -29px"
          v-if="!logo"
        >
          Search
        </div>
        <q-input
          dense
          rounded
          outlined
          v-model="search"
          input-class="text-center"
          placeholder="Artist / Album / Title"
          bgColor="white"
          class="b-input"
        >
        </q-input>
        <q-btn
          dense
          no-caps
          class="q-mt-md b-btn"
          unelevated
          rounded
          @click="onSearch"
        >
          <span class="Search"> Search </span>
        </q-btn>
      </div>
    </div>
  </q-page>
</template> 
<script>
export default {
  props: {
    logo: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      search: "",
    };
  },
  methods: {
    async onSearch() {
      const response = await fetch(
        "https://itunes.apple.com/search?term=" + this.search + "&limit=5"
      );
      const data = await response.json();
      this.$store.commit("search/setSearch", data.results);
      this.$router.push(
        "/detail/" + this.search.replace(/\s+/g, "+").toLowerCase()
      );
      this.$emit("onSearch");
    },
  },
};
</script>
