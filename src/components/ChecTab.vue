<template>
  <button
    class="chec-tab"
    :class="{ 'chec-tab--active': active, 'chec-tab--dark': dark }"
    :disabled="disabled"
    @click="handleClick"
  >
    <!--
      @slot Text to display within the tab button
      @binding disabled Whether the tab is disabled
      @binding active Whether the tab is active
    -->
    <slot v-bind="{ active, disabled }" />
  </button>
</template>

<script>
export default {
  name: 'ChecTab',
  props: {
    /**
     * If this tab should appear selected (active)
     */
    active: Boolean,
    /**
     * Disables the tab (but not the click handler)
     */
    disabled: Boolean,
    /**
     * Show the dark-mode variant of a tab
     */
    dark: Boolean,
  },
  methods: {
    handleClick() {
      /**
       * Emitted the tab is clicked
       * @event click
       * @type {$event}
       */
      this.$emit('click');
    },
  },
};
</script>

<style lang="scss">
.chec-tab {
  // Spacing
  @apply border-b-2 px-4 py-3 font-bold font-lato caps-xxs border-white bg-white text-gray-500;

  &:hover:enabled {
    @apply border-gray-300 bg-gray-100 text-gray-600;
  }

  &:disabled {
    @apply opacity-50 cursor-not-allowed;
  }

  &--active,
  &:active,
  &:focus {
    &:enabled {
      @apply outline-none border-gray-500 text-gray-600;
    }
  }

  &--dark {
    @apply border-gray-500 bg-gray-500 text-gray-300;

    &:hover:enabled {
      @apply border-gray-400 bg-gray-600 text-white;
    }

    &.chec-tab--active,
    &:active,
    &:focus {
      &:enabled {
        @apply border-white text-white;
      }
    }
  }
}
</style>
