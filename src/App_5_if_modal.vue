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

  <div>
    <img class="room-img" src="./assets/images/room0.jpg">
    <!-- 이미 v-if문을 통해 세팅 해뒀으니 isModalOpen 데이터 값을 true로 바꾸면 모달창이 열림 -->
    <h4 @click="isModalOpen = true">{{ products[0] }}</h4>
    <p>{{ price1 }} 만원</p>
    <button v-on:click="reportCnt[0]++">신고</button> <span>신고수 : {{ reportCnt[0] }}</span>
  </div>
  <div>
    <img class="room-img" src="./assets/images/room1.jpg">
    <h4>{{ products[1] }}</h4>
    <p>{{ price2 }} 만원</p>
    <button @click="reportCnt[1]++">신고</button> <span>신고수 : {{ reportCnt[1] }}</span>
  </div>
  <div>
    <img class="room-img" src="./assets/images/room2.jpg">
    <h4>{{ products[2] }}</h4>
    <p>{{ price3 }} 만원</p>
    <button @click="reportCnt[2]++">신고</button> <span>신고수 : {{ reportCnt[2] }}</span>
  </div>

</template>

<script>
// 동적 UI 만드는 법
// 0. UI 디자인 구현
// 1. UI 의 현재 상태를 데이터로 저장해둠
// 2. 데이터에 따라 UI 가 어떻게 보일지 작성
export default {
  name: "App",
  data() {
    return {
      isModalOpen: false, // 1. UI 의 현재 상태를 데이터로 저장. react 에서는 state 라고 함
      price1: 60,
      price2: 150,
      price3: 80,
      products: ['역삼동 원룸', '천호동 원룸', '마포구 원룸'],
      menu: ['Home', 'Products', 'About'],
      reportCnt: [0, 0, 0],
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
