<template>
  <div>
    <router-view></router-view>
    <notifications group="auth" position="top center" />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  name: "App"
});
</script>
