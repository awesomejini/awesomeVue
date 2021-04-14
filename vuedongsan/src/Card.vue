<template>
  <div>
    <img class="room-img" :src="원룸.image" />
    <h4 @click="send" style="cursor: pointer">{{ 원룸.title }}</h4>
    <p>{{ 원룸.price }}원</p>
    <!-- <button @click="inclease(i)">허위매물신고</button>
    <span>신고수 : {{ 신고수[i] }}</span> -->
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    원룸: Object,
  },
  methods: {
    send() {
      this.$emit("openModal", this.원룸.id);
    },
  },
};
</script>

<style>
</style>