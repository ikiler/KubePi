<template>
  <div class="content-container">
    <div class="content-container__header" v-if="$slots.header || header">
      <slot name="header">
        <back-button :path="backPath" :name="backName" :to="backTo" :back="back" v-if="showBack"></back-button>
        {{ header }}
      </slot>
    </div>
    <div class="content-container__toolbar" v-if="$slots.toolbar">
      <slot name="toolbar"></slot>
    </div>
    <slot></slot>
  </div>
</template>

<script>
import BackButton from "@/components/back-button/back-button"
export default {
  name: "LayoutContent",
  components: { BackButton },
  props: {
    header: String,
    description: String,
    backPath: String,
    backName: String,
    backTo: Object,
    back: {
      type: Boolean,
      default:false,
    }
  },
  computed: {
    showBack({backPath, backName, backTo,back}) {
      return backPath || backName || backTo || back
    }
  }
}
</script>

<style lang="scss">
  @import "~@/styles/common/mixins.scss";
  @import "~@/styles/common/variables";

  .content-container {
    transition: 0.3s;
    color: $--color-text-primary;
    background-color: $--color-bg-primary;
    overflow: auto;
    height: 100%;
    padding: 20px;

    .content-container__header {
      line-height: 60px;
      font-size: 18px;
      color: $--color-text-primary;
    }

    .content-container__toolbar {
      @include flex-row(space-between, center);
      margin-bottom: 10px;
    }
  }
</style>
