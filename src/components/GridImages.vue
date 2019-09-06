<template>
  <div>
    <md-card class="md-card-example md-elevation-5" v-for="image in this.images" :key="image.id">
      <md-card-area md-inset>
        <md-card-media md-ratio="16:9">
          <img :src="image.url_n" alt="Coffee House" />
        </md-card-media>

        <md-card-header>
          <h2 class="md-title">{{ image.title.substring(0,22) }}</h2>
          <div class="md-subhead">
            <span>{{ image.ownername.substring(0,30) }}</span>
          </div>
        </md-card-header>
      </md-card-area>

      <!-- <md-card-content>
          <md-button>5:30PM</md-button>
          <md-button>7:30PM</md-button>
          <md-button>9:00PM</md-button>
      </md-card-content>-->
    </md-card>
  </div>
</template>

<script>
export default {
  name: "GridImages",
  props: ["images"]
};
</script>

<style scoped>
.md-card {
  width: 320px;
  margin: 4px;
  display: inline-block;
  vertical-align: top;
}
</style>