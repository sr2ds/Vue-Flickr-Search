<template>
  <div id="app">
    <md-progress-bar md-mode="indeterminate" v-if="loading"></md-progress-bar>

    <md-toolbar class="md-primary">
      <h1 class="md-title">Vue Flickr Search with Material Ui</h1>
    </md-toolbar>

    <md-content>
      <md-field>
        <label>Search</label>
        <md-input v-model="search" v-on:keyup.13="handleSubmit"></md-input>
      </md-field>
      <GridImages :images="images" />
    </md-content>

    <LoadMore :show="this.images.length" @loadMore="loadMore" />
    
  </div>
</template>

<script>
import { flickrSearch } from "@/services/flickr";
import GridImages from "@/components/GridImages";
import LoadMore from "@/components/LoadMore";

export default {
  name: "app",
  components: {
    GridImages,
    LoadMore
  },
  data() {
    return {
      search: "",
      images: [],
      loading: false,
      page: 1
    };
  },
  methods: {
    handleSubmit() {
      this.loading = true;

      if (!this.search) {
        this.images = [];
        this.loading = false;
        this.page = 1;
        return;
      }

      flickrSearch(this.search)
        .then(response => response.json())
        .then(data => {
          (this.images = data.photos.photo), (this.loading = false);
        });
    },

    loadMore() {
      this.loading = true;
      this.page = this.page + 1;
      flickrSearch(this.search, this.page)
        .then(response => response.json())
        .then(data => {
          this.images = this.images.concat(data.photos.photo);
          this.loading = false;
        });
    }
  }
};
</script>


<style scoped>
.md-content {
  padding: 16px;
}
.md-primary {
  margin: 0 auto;
}
</style>
