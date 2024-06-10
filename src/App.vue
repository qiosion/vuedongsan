<template>
  <!-- 모달창 -> v-if="조건식" 사용. 참일 때만 html을 보여줌 -->
  <div class="black-bg" v-if="isModalOpen">
    <div class="white-bg">
      <h4>상세 페이지</h4>
      <p>상세 페이지 내용</p>
      <button @click="isModalOpen = false">닫기</button>
    </div>
  </div>

  <div class="menu">
    <a v-for="i in menu" :key="i">{{ i }}</a>
  </div>

  <div v-for="(a, i) in onerooms" :key="i">
    <img class="room-img" :src="onerooms[i].image">
    <!-- 이미 v-if문을 통해 세팅 해뒀으니 isModalOpen 데이터 값을 true로 바꾸면 모달창이 열림 -->
    <h4 @click="isModalOpen = true">{{ onerooms[i].title }}</h4>
    <p>{{ onerooms[i].price }} 원</p>
  </div>

</template>

<script>
import data from './assets/oneroom.js';
// default 로 export 했으므로 import할 때 사용할 변수명은 마음대로 해도 됨
// 만약 export { var1, var2,.. } 이런식으로 했다면 import { var1 } 처럼 지정해줘야함
data; // import 하고 안쓰면 에러뜨니까 어디서든 써줘야함

export default {
  name: "App",
  data() {
    return {
      isModalOpen: false, // 1. UI 의 현재 상태를 데이터로 저장
      menu: ['Home', 'Products', 'About'],
      onerooms: data,
    };
  },
  methods: { // 함수
    
  },
  components: {},
};
</script>

<style>
body {
  margin: 0;
}

div {
  box-sizing: border-box;
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

.room-img {
  width: 100%;
  margin-top: 40px;
}

.menu {
  background-color: rgb(42, 56, 117);
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
