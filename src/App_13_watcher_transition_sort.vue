<template>
  <div class="menu">
    <a v-for="i in menu" :key="i">{{ i }}</a>
  </div>

  <Discount v-bind="Object" />

<!--
    vue 는 데이터 바인딩 해두면 HTML에 데이터가 실시간으로 반영됨
    데이터를 정렬하고싶다면 그냥 sort() 함수 쓰면 됨
-->
  <div style="text-align: right;">
    <button class="btn" @click="priceSort">가격순정렬</button>
    <button class="btn" @click="priceReverse">가격역정렬</button>
    <button class="btn" @click="titleSort">가나다정렬</button>
    <button class="btn" @click="sortBack">되돌리기</button>
  </div>

  <Transition name="fade">
    <Modal :onerooms="onerooms" :clicked="clicked" :isModalOpen="isModalOpen"
    @closeModal="isModalOpen = false"/>
  </Transition>

  <Card @openModal="isModalOpen = true; clicked = $event"
  v-for="(oneroom, i) in onerooms"
  :key="i"
  :oneroom="onerooms[i]" />

</template>

<script>
import data from './assets/oneroom.js';
import Discount from './components/Discount.vue';
import Modal from './components/Modal.vue';
import Card from './components/Card.vue';

export default {
  name: "App",
  data() {
    return {
      Object: {
        name: 'kim',
        age: 20,
      },
      clicked: 0, // 클릭한 제목
      isModalOpen: false, // 1. UI 의 현재 상태를 데이터로 저장
      menu: ['Home', 'Products', 'About'],
      onerooms: data, // [{}. {}. {}, ...]
      oneroomsOriginal: [...data], // 원본데이터 보존
      // array, object 데이터의 별개의 사본을 만드려면 [...array] 를 써야함
    };
  },
  methods: { // 함수
    /*
    sort() : 원본 데이터 변경시킴. 문자 정렬. 숫자 정렬 하고싶으면 아래 방식을 써야 함
    reverse() : 역정렬

    var array = [3, 6, 2];
    array.sort(function(a, b) { // a, b 는 배열 안의 요소들
      return a - b; // 둘 사이의 차이가 음수면 a 를 왼쪽으로 이동하는 방식(버블정렬)
    })
    */
    priceSort() { // 가격 순정렬
      this.onerooms.sort(function(a, b) {
        return a.price - b.price; // 가격 간 비교
      })
    },
    priceReverse() { // 가격 역정렬
      this.onerooms.reverse(function(a, b) {
        return a.price - b.price; // 가격 간 비교
        // 또는 sort 함수 쓰되 b - a 하면 됨
      })
    },
    titleSort() { // 가나다 순정렬
      this.onerooms.sort(function(a, b) {
        return a.title.localeCompare(b.title);
      })
    },
    sortBack() { // 정렬 되돌리기
      // 등호로 array 를 집어넣으면 서로간의 값 공유가 됨
      // 그러므로 개별 복사본을 만들어서 집어넣어야함
      this.onerooms = [...this.oneroomsOriginal];
    }
  },
  components: {
    Discount: Discount,
    Modal,
    Card,
  },
};
</script>

<style>
/* 등장 */
.fade-enter-from { /* 시작 */
  /* opacity: 0; */
  transform: translateY(-1000px); /* y축 -1000px 으로 이동 */
}
.fade-enter-active { /* 중간단계. 트랜지션 등 */
  transition: all 1s;
}
.fade-enter-to { /* 끝 */
  /* opacity: 1; */
  transform: translateY(0px); /* y축 0px 으로 이동. 즉 위에서 밑으로 내려오는 형태 */
}
/* 퇴장 */
.fade-leave-from { /* 시작 */
  opacity: 1;
}
.fade-leave-active { /* 중간단계. 트랜지션 등 */
  transition: all 1s;
}
.fade-leave-to { /* 끝 */
  opacity: 0;
}

.start {
  opacity: 0;
  transition: all 1s; /* 모든 속성이 변할 때 1초에 걸쳐서 변화해라 */
}
.end {
  opacity: 1;
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

.btn {
  width: 95px;
  margin: 5px;
  border: 1px solid #ffadb8;
  border-radius: 20px;
  background-color: #f3ffad;
  color: black;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>