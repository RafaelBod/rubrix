<template>
  <a
    class="sidebar-button"
    :class="[type.toLowerCase(), activeView.includes(id) ? 'active' : '']"
    href="#"
    :data-title="!activeView.includes(id) ? tooltip : null"
    @click="$emit('button-action', id)"
  >
    <!-- <svgicon
      v-if="type !== 'Refresh'"
      v-show="activeView.includes(id)"
      class="sidebar-button__icon-help"
      :name="type === 'Mode' ? 'check3' : 'double-chev'"
    ></svgicon> -->
    <svgicon :name="icon"></svgicon>
  </a>
</template>

<script>
import "assets/icons/refresh";
import "assets/icons/explore-view";
import "assets/icons/annotate-view";
import "assets/icons/labelling-rules-view";
import "assets/icons/progress";
import "assets/icons/metrics";
export default {
  props: {
    activeView: {
      type: Array,
      default: () => [],
    },
    tooltip: {
      type: String,
      required: true,
    },
    id: {
      type: String,
      required: true,
    },
    icon: {
      type: String,
      required: true,
    },
    type: {
      type: String,
      required: true,
      validator: (value) => {
        return ["Mode", "Metrics", "Refresh"].includes(value);
      },
    },
  },
};
</script>

<style lang="scss" scoped>
$color: #333346;
.sidebar-button {
  &__icon-help {
    left: 5px;
    width: 11px !important;
    margin-right: 0;
    stroke-width: 2;
    position: absolute;
    left: 0.8em;
  }
  &.active {
    &.mode {
      .svg-icon {
        background: palette(grey, smooth);
        border-radius: $border-radius;
      }
    }
    &.metrics {
      position: relative;
      &:before {
        content: "";
        height: 38px;
        width: 2px;
        background: $color;
        border-radius: 2px;
        position: absolute;
        left: 0;
        top: 0;
      }
    }
  }
}
.svg-icon {
  display: block;
  text-align: center;
  margin: auto;
  width: 24px;
  height: 24px;
  fill: $color;
  padding: 0.5em;
  box-sizing: content-box;
  margin-bottom: 0.5em;
}
</style>
