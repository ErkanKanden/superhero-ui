<template>
  <div class="right-section-title">
    <span><slot /></span>

    <button
      v-if="toggleHandler"
      @click="toggleHandler"
    >
      <IconExpanded :class="{ closed }" />
    </button>
  </div>
</template>

<script>
import IconExpanded from '../../assets/iconExpanded.svg?icon-component';

export default {
  components: { IconExpanded },
  props: {
    closed: Boolean,
    toggleHandler: { type: Function, default: null },
  },
};
</script>

<style lang="scss" scoped>
.right-section-title {
  color: $standard_font_color;
  font-weight: 600;
  padding-bottom: 0.65rem;
  display: flex;
  justify-content: space-between;

  img {
    height: 1.2rem;
    margin-right: 0.2rem;
  }

  button {
    color: $light_font_color;
    background: none;
    border: none;
    outline: none;
    padding: 0;

    &:hover {
      color: $lighter_font_color;
    }

    svg {
      height: 1em;

      &.closed {
        transform: rotate(180deg);
      }
    }
  }
}
</style>
