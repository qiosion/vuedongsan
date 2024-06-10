<template>
  <div class="menu">
    <a v-for="i in menu" :key="i">{{ i }}</a>
  </div>

  <Discount v-bind="Object" />

<!--
    css 로 애니메이션 주기
        1. 애니메이션 시작 전 클래스 명과 애니메이션 끝난 후 클래스 명을 설정
        2. 원할 때마다 클래스명을 붙이면 됨

    isModalOpen 이 true일 때 end class 를 추가하고 싶다 -> 클래스에 데이터바인딩
        :class="{ 붙이고싶은 클래스명: 조건식 }"
        <div class="start" :class="{ end: isModalOpen }">
    
    vue 에서 제공하는 Transition 태그를 이용하면 쉬움
        1. 애니메이션 주고싶은 요소를 <Transition name="변수명">으로 감싸기
        2. 스타일에서 클래스명 3+3 개 작성
            > 등장
                변수명-enter-from : 시작 시 스타일
                변수명-enter-active : 중간단계. 트랜지션 등을 작성
                변수명-enter-to : 끝날 시 스타일
            > 퇴장
                변수명-leave-from : 시작 시 스타일
                변수명-leave-active : 중간단계. 트랜지션 등을 작성
                변수명-leave-to : 끝날 시 스타일
-->

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
      onerooms: data,
    };
  },
  methods: { // 함수
    
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
  opacity: 0;
}
.fade-enter-active { /* 중간단계. 트랜지션 등 */
  transition: all 1s;
}
.fade-enter-to { /* 끝 */
  opacity: 1;
}
/* 퇴장 */
.fade-leave-from { /* 시작 */
  /* opacity: 1; */
  transform: translateY(-1000px); /* y축으로 -1000px 이동해줘 */
}
.fade-leave-active { /* 중간단계. 트랜지션 등 */
  transition: all 1s;
}
.fade-leave-to { /* 끝 */
  transform: translateY(0px); /* y축으로 -1000px 이동해줘 */
  /* opacity: 0; */
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

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>