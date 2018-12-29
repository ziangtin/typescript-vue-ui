<template>
    <div :style="containerStyle"
         :class="{ on: value }"
         @click="$emit('input', !value)">
        <span :style="buttonStyle" />
    </div>
</template>


<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
const UNIT = 'px';
const toSize = (n: number): string => `${n}${UNIT}`;

@Component
export default class SwitchBtn extends Vue {
  @Prop({ default: false }) private value!: boolean;
  @Prop({ default: 60 }) private width!: number;
  @Prop({ default: 30 }) private height!: number;

  get containerStyle(): object {
    return {
      width: toSize(this.width),
      height: toSize(this.height),
      'border-radius': toSize(this.height / 2)
    };
  }
  get buttonStyle(): object {
    return {
      width: toSize(this.height),
      height: toSize(this.height)
    };
  }
}
</script>

<style lang="less" scoped>
@transition-duration: 0.25s;

.transition-action {
  transition-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
  transition-duration: @transition-duration;
}

.container-transition {
  transition-property: background;
  .transition-action();
}

.button-transition {
  transition-property: box-shadow, left, transform;
  .transition-action();
}

div {
  display: inline-block;
  background-color: #ffffff;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.1);
  position: relative;
  .container-transition();
  cursor: pointer;

  span {
    display: block;
    background-color: #ffffff;
    border-radius: 50%;
    box-shadow: 1px 0 8px rgba(0, 0, 0, 0.3);
    transform: translateX(0);
    position: absolute;
    top: 0;
    left: 0;
    .button-transition();
    outline: none;
    z-index: 1;
  }

  &.on {
    justify-content: flex-end;
    background: #60bb62;
    .container-transition();

    span {
      left: 100%;
      transform: translateX(-100%);
      box-shadow: -1px 0 8px rgba(0, 0, 0, 0.3);
      .button-transition();
    }
  }
}
</style>
