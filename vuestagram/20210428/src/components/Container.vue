<template>
  <div>
    <div v-if="step == 0">
      <Post v-for="(a, i) in 게시물" :key="a.name" :게시물="게시물[i]" :i="i" />
    </div>

    <!-- 필터선택페이지 -->
    <div v-if="step == 1">
      <div
        :class="`${선택한필터} upload-image`"
        :style="`background: url(${업로드한파일}) top center; background-size: 100%;`"
      ></div>
      <div class="filters">
        <FilterBox
          v-for="필터 in 필터들"
          :업로드한파일="업로드한파일"
          :key="필터"
          :필터="필터"
        >
          <span>{{ 필터 }}</span>
        </FilterBox>
      </div>
    </div>

    <!-- 글작성페이지 -->
    <div v-if="step == 2">
      <div
        :class="`${선택한필터} upload-image`"
        :style="`background: url(${업로드한파일}) top center; background-size: 100%;`"
      ></div>
      <div class="write">
        <textarea
          class="write-box"
          v-model="내가입력한글"
          @change="$emit('mytext', 내가입력한글)"
          placeholder="White here!"
        ></textarea>
      </div>
    </div>
  </div>
</template>

<script>
import Post from "./Post";
import FilterBox from "./FilterBox";

export default {
  name: "Container",
  data() {
    return {
      내가입력한글: "",
      필터들: [
        "default",
        "aden",
        "_1977",
        "brannan",
        "brooklyn",
        "clarendon",
        "earlybird",
        "gingham",
        "hudson",
        "inkwell",
        "kelvin",
        "lark",
        "lofi",
        "maven",
        "mayfair",
        "moon",
        "nashville",
        "perpetua",
        "reyes",
        "rise",
        "slumber",
        "stinson",
        "toaster",
        "valencia",
        "walden",
        "willow",
        "xpro2",
      ],
    };
  },
  components: {
    Post,
    FilterBox,
  },
  props: {
    게시물: Array,
    step: Number,
    업로드한파일: String,
    선택한필터: String,
  },
};
</script>

<style>
.upload-image {
  width: 100%;
  height: 450px;
  background: cornflowerblue;
  background-size: cover;
}
.filters {
  overflow-x: scroll;
  white-space: nowrap;
}
.filter-1 {
  width: 100px;
  height: 100px;
  background-color: cornflowerblue;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color: white;
  background-size: cover;
}
.filters::-webkit-scrollbar {
  height: 5px;
}
.filters::-webkit-scrollbar-track {
  background: #f1f1f1;
}
.filters::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
  background: #555;
}
.write-box {
  border: none;
  width: 90%;
  height: 100px;
  padding: 15px;
  margin: auto;
  display: block;
  outline: none;
}
</style>