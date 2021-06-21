<template>
  <button type="button" :class="classes" @click="onClick" :style="style">
    {{ text }}
  </button>
</template>
<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class MaButton extends Vue {
  @Prop() text!: string;
  @Prop() color!: "green" | "blue";
  @Prop() frameOnly!: boolean;
  @Prop() width!: string;
  @Prop() height!: string;
  @Prop() fontFamily!: string;
  @Prop() fontSize!: string;
  @Prop() disabled!: boolean;
  @Prop() loading!: boolean;

  onClick(): void {
    this.$emit("click");
  }

  get classes(): string {
    let classes = "ma-button ";
    classes += (this.color ? this.color : "green") + " ";
    classes += this.frameOnly ? "frame-only " : "";
    classes += this.loading || this.disabled ? "disabled" : "";
    return classes;
  }

  get style(): string {
    let style = "";
    if (this.height) style += `height: ${this.height};`;
    if (this.width) style += `width: ${this.width};`;
    if (this.fontFamily) style += `font-family: ${this.fontFamily};`;
    if (this.fontSize) style += `font-size: ${this.fontSize};`;
    return style;
  }
}
</script>

<style scoped lang="scss">
@import "../../assets/scss/setup.scss";
.ma-button {
  font-family: heebo-Black, sans-serif;
  font-weight: 400;
  border-radius: 100px;
  color: #ffffff;
  cursor: pointer;
  border: none;
  padding: 10px;
  min-width: 100px;
  &.green {
    background-color: #18c746;
    &.disabled {
      cursor: auto;
      background-color: #88ddb4;
      color: #ffffff;
    }
    &.frame-only {
      background-color: transparent;
      border: 1px solid #18c746;
      color: #18c746;
      &.disabled {
        cursor: auto;
      }
    }
  }
  &.blue {
    background-color: #0084f4;
    &.disabled {
      cursor: auto;
      background-color: #9bc0e0;
      color: #ffffff;
    }
    &.frame-only {
      background-color: transparent;
      border: 1px solid #0084f4;
      color: #0084f4;
      &.disabled {
        cursor: auto;
      }
    }
  }
}
</style>
