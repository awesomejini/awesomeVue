<template>
  <div class="header">
    <ul class="header-button-left">
      <li v-if="step == 1 || step == 2" @click="step = 0">Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="step == 1" @click="step++">Next</li>
      <li v-if="step == 2" @click="publish">발행</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <!-- <h4>안녕 {{ $store.state.name }}</h4>
  <button @click="$store.commit('이름변경')">이름버튼</button>
  <h4>내 나이는 {{ $store.state.age }}</h4>
  <button @click="$store.commit('나이변경', 10)">나이버튼</button> -->

  <!-- <p>{{ $store.state.more }}</p>
  <button @click="$store.dispatch('getData')">더보기 버튼</button> -->

  <!-- <p>{{ 내이름 }} {{ age }} {{ likes }}</p> -->

  <Container
    @mytext="내가입력한글 = $event"
    :게시물="게시물"
    :step="step"
    :업로드한파일="업로드한파일"
    :선택한필터="선택한필터"
  />

  <button v-if="step == 0" @click="more">더보기</button>

  <div class="footer">
    <ul class="footer-button-plus">
      <input
        @change="upload"
        accept="image/*"
        type="file"
        id="file"
        class="inputfile"
      />
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>

  <!-- tap -->
  <!-- <div v-if="step == 0">내용0</div>
  <div v-if="step == 1">내용1</div>
  <div v-if="step == 2">내용2</div>
  <button @click="step = 0">버튼0</button>
  <button @click="step = 1">버튼1</button>
  <button @click="step = 2">버튼2</button> -->
</template>

<script>
import Container from "./components/Container";
import postdata from "./assets/postdata";
import axios from "axios";
axios.get();
import moment from "moment";
import { mapMutations, mapState } from "vuex";

export default {
  name: "App",
  data() {
    return {
      게시물: postdata,
      더보기: 0,
      step: 0,
      업로드한파일: "",
      내가입력한글: "",
      선택한필터: "",
      오늘날짜: "",
      카운터: 0,
    };
  },
  mounted() {
    this.emitter.on("필터선택", (a) => {
      this.선택한필터 = a;
    });
    var today = moment().format("MMM DD");
    this.오늘날짜 = today;
  },
  components: {
    Container,
  },

  computed: {
    name() {
      return this.$store.state.name;
    },
    ...mapState(["name", "age", "likes"]),
    ...mapState({ 내이름: "name" }),
  },

  methods: {
    ...mapMutations(["setMore", "좋아요"]),
    more() {
      axios
        .get(`https://codingapple1.github.io/vue/more${this.더보기}.json`)
        .then((result) => {
          this.게시물.push(result.data);
          this.더보기++;
        });
    },
    upload(e) {
      let 파일 = e.target.files;
      console.log(파일[0]);
      let url = URL.createObjectURL(파일[0]);
      this.업로드한파일 = url;
      this.step++;
    },
    publish() {
      var 내게시물 = {
        name: "Awosome jini",
        userImage:
          "https://joshua1988.github.io/images/posts/web/vuejs/logo.png",
        postImage: this.업로드한파일,
        likes: 0,
        date: this.오늘날짜,
        liked: false,
        content: this.내가입력한글,
        filter: this.선택한필터,
      };
      this.게시물.unshift(내게시물);
      this.step = 0;
    },
  },
};
</script>

<style>
body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
</style>
