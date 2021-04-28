<template>
  <div
    :class="`${필터} filter-item`"
    :style="`background: url(${업로드한파일}) top center; background-size: 100%;`"
  >
    <slot></slot>
    <button @click="fire">버튼</button>
  </div>
</template>

<script>
export default {
  name: "filterbox",
  methods: {
    fire() {
      this.emitter.emit("필터선택", this.필터);
    },
  },
  props: {
    업로드한파일: String,
    필터: String,
  },
};
</script>

<style>
.filter-item {
  width: 100px;
  height: 100px;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color: white;
  background-size: cover;
  background-position: center;
}
</style>