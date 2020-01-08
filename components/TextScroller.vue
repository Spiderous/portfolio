<template>
  <section class="text-scroller">
    <span>I create</span>

    <span class="wrapper">
      <transition name="current">
        <span class="current-creation" v-if="!switching">{{ currentCreation }}</span>
      </transition>
    </span>
  </section>
</template>

<script>
export default {
  data: () => ({
    creations: ["websites", "native apps", "web designs", "backend apps"],
    currentIndex: 0,
    switching: false
  }),
  computed: {
    currentCreation() {
      return this.creations[this.currentIndex];
    }
  },
  mounted() {
    setInterval(() => {
      this.switching = true;

      setTimeout(() => {
        this.currentIndex = (this.currentIndex + 1) % this.creations.length;
        this.switching = false;
      }, 200);
    }, 3000);
  }
};
</script>

<style lang="scss" scoped>
@import "@/assets/scss/variables";
@import "@/assets/scss/responsive";

.text-scroller {
  display: flex;
}

.wrapper {
  margin-left: 10px;

  position: relative;

  display: flex;
  align-items: center;

  overflow: hidden;
}

.current-creation {
  color: $primary;
}

// Vue animation class
.current {
  $animDuration: 200ms;

  &-leave {
    transform: translate(0);
    opacity: 1;
  }

  &-enter {
    transform: translateY(20px);
    opacity: 0;
  }

  &-leave-active,
  &-enter-active {
    transition: opacity $animDuration, transform $animDuration;
  }

  &-leave-to {
    transform: translateY(-20px);
    opacity: 0;
  }
}

// Responsiveness
@include medium() {
  .text-scroller {
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .wrapper {
    margin: 0;
  }
}
</style>