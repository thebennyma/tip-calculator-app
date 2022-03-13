<template>
  <div class="home">
    <div class="home__title">
      <span>SPLI</span>
      <span>TTER</span>
    </div>
    <PxTipComponent />
    <div class="attribution">
      Challenge by
      <a href="https://www.frontendmentor.io?ref=challenge" target="_blank"
        >Frontend Mentor</a
      >. Coded by
      <a href="https://github.com/thebennyma" target="_blank"
        >Marco Antonio Alvarado</a
      >.
    </div>
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
  @media only screen and (max-width: 450px) {
    margin: 0;
    width: 100%;
  }
  &__title {
    display: grid;
    font-family: "Space Mono", monospace;
    font-weight: bold;
    font-size: 1.6rem;
    text-align: center;
    color: hsl(186, 14%, 43%);
    letter-spacing: 8px;
    margin-bottom: 4rem;
  }
  .attribution {
    font-family: "Space Mono", monospace;
    font-weight: bold;
    font-size: 1rem;
    text-align: center;
    color: hsl(186, 14%, 43%);
    margin-top: 4rem;
  }
  &__title,
  .attribution {
    @media only screen and (max-width: 450px) {
      margin-top: 2rem;
      margin-bottom: 2rem;
    }
  }
}
</style>
