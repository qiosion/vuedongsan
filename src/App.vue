<template>
  <div class="menu">
    <a v-for="i in menu" :key="i">{{ i }}</a>
  </div>

<!--
    lifecycle Hook
    컴포넌트의 라이프사이클 : 컴포넌트가 웹페이지에 표시되기까지 거치는 단계
        1. create 단계 : 데이터만 존재
        2. mount 단계 : template 에 있던 것을 실제 HTML 로 바뀜. 화면에 뜬 상태
        3. 컴포넌트 생성
        4. update 단계 : 데이터 변화 시 컴포넌트 실시간 재렌더링
        5. unmount 단계 : 컴포넌트 삭제
    
    라이프사이클 중간에 훅 hook 을 걸어서 원하는 코드 실행 가능
    서버에서 데이터 가져올 때도 lifecycle hook 안에 코드를 짬
-->
  <Discount v-if="showDiscount == true" />

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
      showDiscount: true,
      Object: {
        name: 'kim',
        age: 20,
      },
      clicked: 0, 
      isModalOpen: false,
      menu: ['Home', 'Products', 'About'],
      onerooms: data,
      oneroomsOriginal: [...data], // 원본데이터 보존
      // array, object 데이터의 별개의 사본을 만드려면 [...array] 를 써야함
    };
  },
  methods: { // 함수
    priceSort() { // 가격 순정렬
      this.onerooms.sort(function(a, b) {
        return a.price - b.price; // 가격 간 비교
      })
    },
    priceReverse() { // 가격 역정렬
      this.onerooms.reverse(function(a, b) {
        return a.price - b.price; // 가격 간 비교
      })
    },
    titleSort() { // 가나다 순정렬
      this.onerooms.sort(function(a, b) {
        return a.title.localeCompare(b.title);
      })
    },
    sortBack() { // 정렬 되돌리기
      this.onerooms = [...this.oneroomsOriginal];
    }
  },
  components: {
    Discount: Discount,
    Modal,
    Card,
  },
  // lifecycle hook. 각 컴포넌트에 설정가능
  created() { // html 생성 전 데이터만 존재할 때
    // 서버에서 데이터 가져오는 코드는 created, mounted 에 작성
  },
  mounted() { // 마운트 되고 나서 실행
    // this 쓸 때 화살표 함수 써야 에러가 안남
    setTimeout(() => { // 지정 시간 후 실행
      this.showDiscount = false;
    }, 30000); // 30초

    
  },
  beforeMount() { // 마운트 되기 전에 실행

  },
};
</script>

<style>
/* 등장 */
.fade-enter-from { /* 시작 */
  transform: translateY(-1000px);
}
.fade-enter-active { 
  transition: all 1s;
}
.fade-enter-to { /* 끝 */
  transform: translateY(0px);
}
/* 퇴장 */
.fade-leave-from { /* 시작 */
  opacity: 1;
}
.fade-leave-active {
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