<template>
  <div>
    <div class="row">
      <div class="col-12 text-center">
        <span class="Search-result-for-"> Search result for : </span>
        <span class="Json-Mraz">
          {{ $route.params.search.replace(/\+/g, " ") }}
        </span>
      </div>
    </div>

    <q-card
      class="card-Rectangle"
      v-for="(row, index) in getSearch"
      :key="index"
    >
      <q-item>
        <q-item-section>
          <img :src="row.artworkUrl100" class="imground" />
        </q-item-section>

        <q-item-section>
          <q-item-label caption>
            {{ row.artistName.substring(0, 15) + "..." }}</q-item-label
          >
          <q-item-label class="text-bold">
            {{ row.collectionName?.substring(0, 20) + "..." ?? "" }}
          </q-item-label>

          <div class="row q-mt-lg">
            <div class="col-8">
              <q-badge
                rounded
                color="green-8"
                :label="row.primaryGenreName.substring(0, 15)"
              />
            </div>
            <div class="col-1 q-pl-sm q-mr-sm">
              <img
                src="~assets/currency-dollar_2022-08-13/currency-dollar.png"
              />
            </div>
            <div class="col-1 q-pl-sm">
              <span class="span"> {{ row.trackPrice }} </span>
            </div>
          </div>
        </q-item-section>
      </q-item>
    </q-card>

    <div class="text-center">
      <q-btn
        dense
        no-caps
        class="q-mt-md b-btnMore"
        unelevated
        rounded
        @click="LoadMore"
      >
        <span class="Load-More"> Load More </span>
      </q-btn>
    </div>
  </div>
</template>
<script>
import { mapGetters } from "vuex";
export default {
  data() {
    return {
      result: [],
      limit: 5,
    };
  },
  computed: {
    ...mapGetters({
      getSearch: "search/getSearch",
    }),
  },
  methods: {
    async searchResult(limit) {
      const response = await fetch(
        "https://itunes.apple.com/search?term=" +
          this.$route.params.search +
          "&limit=" +
          limit
      );
      const data = await response.json();
      this.$store.commit("search/setSearch", data.results);
    },
    LoadMore() {
      this.searchResult(this.getSearch.length + 5);
    },
  },
};
</script>