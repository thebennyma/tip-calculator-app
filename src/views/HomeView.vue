<template>
  <div class="home">
    <PxTipComponent />
  </div>
</template>

<script>
import PxTipComponent from "@/components/PxTipComponent.vue";

export default {
  name: "HomeView",
  components: { PxTipComponent },
  data() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
.home {
  margin: 1rem;
  width: min-content;
  height: min-content;
  justify-self: center;
}
</style>
