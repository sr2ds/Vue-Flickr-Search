<template>
  <div>
    <md-speed-dial class="md-bottom-right" md-direction="bottom" v-if="this.show">
      <md-speed-dial-target class="md-primary" v-on:click="loadMore">
        <md-icon>add</md-icon>
      </md-speed-dial-target>
    </md-speed-dial>
  </div>
</template>

<script>
export default {
  name: "LoadMore",
  props: ["show"],
  methods: {
    loadMore() {
      this.$emit("loadMore");
    }
  }
};
</script>