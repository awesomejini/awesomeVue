<template>
  <div v-if="1 == 2">안녕하세요</div>
  <div v-else-if="1 == 3">안녕하세요2</div>

  <!-- 모달창 1 -->
  <!-- <div class="start" :class="{ end: 모달창열렸니 }">
    <Modal
      @closeModal="모달창열렸니 = $event"
      :원룸들="원룸들"
      :누른거="누른거"
      :모달창열렸니="모달창열렸니"
    />
  </div> -->

  <!-- 모달창 2 -->
  <transition name="fade">
    <Modal
      @closeModal="모달창열렸니 = $event"
      :원룸들="원룸들"
      :누른거="누른거"
      :모달창열렸니="모달창열렸니"
    />
  </transition>

  <div class="menu">
    <a v-for="(a, i) in 메뉴들" :key="i">{{ a }}</a>
  </div>

  <Discount
    v-bind="오브젝트"
    :이름="오브젝트.name"
    :나이="오브젝트.age"
    :discountNum="discountNum"
  />

  <button @click="priceSortLow">가격낮은순정렬</button>
  <button @click="priceSortHigh">가격높은순정렬</button>
  <button @click="priceSortTitle">가나다순정렬</button>
  <button @click="sortBack">되돌리기</button>

  <Card
    @openModal="
      모달창열렸니 = true;
      누른거 = $event;
    "
    :원룸="원룸들[i]"
    v-for="(a, i) in 원룸들"
    :key="i"
  />

  <!-- <div v-for="(a, i) in 원룸들" :key="i">
    <img class="room-img" :src="a.image" />
    <h4
      @click="
        모달창열렸니 = true;
        누른거 = i;
      "
      style="cursor: pointer"
    >
      {{ a.title }}
    </h4>
    <p>{{ a.price }}원</p>
    <button @click="inclease(i)">허위매물신고</button>
    <span>신고수 : {{ 신고수[i] }}</span>
  </div> -->

  <!-- <div>
    <h4 class="red" :style="스타일">{{ products[0] }}</h4>
    <p>{{ price[0] }} 만원</p>
    <button @click="inclease">허위매물신고</button>
    <span>신고수 : {{ 신고수 }}</span>
  </div>
  <div>
    <h4>{{ products[1] }}</h4>
    <p>{{ price[1] }} 만원</p>
  </div>
  <div>
    <h4>{{ products[2] }}</h4>
    <p>{{ price[2] }} 만원</p>
  </div> -->
</template>

<script>
import data from "./assets/oneroom.js";
import Discount from "./Discount.vue";
import Modal from "./Modal.vue";
import Card from "./Card.vue";

export default {
  name: "App",
  data() {
    return {
      discountNum: 30,
      원룸들오리지널: [...data],
      오브젝트: { name: "kim", age: 20 },
      누른거: 0,
      원룸들: data,
      모달창열렸니: false,
      price: [60, 70, 80],
      스타일: "color: blue",

      신고수: [0, 0, 0, 0, 0, 0],
      메뉴들: ["Home", "Shop", "About"],
      products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
    };
  },

  mounted() {
    setInterval(() => {
      if (this.discountNum > 0) {
        this.discountNum--;
      } else {
        clearInterval();
      }
    }, 1000);
  },

  methods: {
    inclease(i) {
      this.신고수[i]++;
    },
    priceSortLow() {
      this.원룸들.sort(function (a, b) {
        return a.price - b.price;
      });
    },
    priceSortHigh() {
      this.원룸들.sort(function (a, b) {
        return b.price - a.price;
      });
    },
    priceSortTitle() {
      this.원룸들.sort(function (a, b) {
        return a.title < b.title ? -1 : a.title > b.title ? 1 : 0;
      });
    },
    sortBack() {
      this.원룸들 = [...this.원룸들오리지널];
    },
  },
  components: {
    Discount: Discount,
    Modal: Modal,
    Card: Card,
  },
};
</script>

<style>
/* .start {
  opacity: 0;
  transition: all 1s;
}

.end {
  opacity: 1;
} */

.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 0.3s;
}
.fade-enter-to {
  opacity: 1;
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 0.3s;
}
.fade-leave-to {
  opacity: 0;
}

body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}
</style>
