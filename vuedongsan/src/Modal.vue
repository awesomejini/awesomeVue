<template>
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <h4>{{ 원룸들[누른거].title }}</h4>
      <img class="room-img" :src="원룸들[누른거].image" />
      <p>{{ 원룸들[누른거].content }}</p>
      <!-- <input @input="month = $event.target.value" /> -->
      <!-- <textarea></textarea> -->
      <!-- <select v-model.number="month">
        <option>1</option>
        <option>2</option>
        <option>3</option>
      </select> -->
      <input v-model="month" type="range" min="1" max="12" />
      <input @keydown.space.prevent v-model="month" />
      <p>{{ month }}개월 선택함 : {{ 원룸들[누른거].price * month }}원</p>
      <button @click="$emit('closeModal', false)">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      month: 3,
    };
  },
  beforeUpdate() {
    if (this.month == 2) {
      alert("3개월부터 가능합니다.");
      this.month = 3;
    }
  },
  watch: {
    month(a) {
      if (isNaN(a) == true) {
        alert("숫자만 입력하세요");
        this.month = 3;
      } else if (a >= 13) {
        alert("12개월까지 가능합니다.");
        this.month = 3;
      }
    },
  },
  props: {
    원룸들: Array,
    누른거: Number,
    모달창열렸니: Boolean,
  },
};
</script>

<style>
</style>