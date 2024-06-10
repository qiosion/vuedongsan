<template>
  <div class="menu">
    <a v-for="i in menu" :key="i">{{ i }}</a>
  </div>

  <Discount v-bind="Object" />

<!-- 
  props 쓰는 법
    1. 부모 컴포넌트에서 v-bind: 또는 : 를 사용하여 보내고싶은 데이터 전송 
        :변수명="전송하고자 하는 데이터(아래에서 설정한 값)"
        colon 은 속성에 데이터 바인딩할 때, props 전송할 때 사용
    2. 자식 컴포넌트에서 default 값에 props 등록
        json 형태로 등록, {데이터 이름: 자료형 이름}
    
  $emit() 함수
    props 는 read-only. 자식 컴포넌트에서 수정하면 에러 발생.
    이때 custom event 로 자식이 메시지 전송하여 해결
      자식 -> 부모 메시지 전송 :$emit('변수명') 또는  $emit('변수명', 데이터)
      부모가 메시지 수신 : @변수명="해당 변수명을 수신했을 때 실행할 js 코드"
                        이때 js 코드 안에서 $event 를 사용하여 받은 데이터를 사용 가능
    $emit() 을 함수 안에 쓰고싶다면 this.$emit()
-->

  <Modal :onerooms="onerooms" :clicked="clicked" :isModalOpen="isModalOpen"
  @closeModal="isModalOpen = false; clicked = $event"/>

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
    // Discount: Discount, // 키와 값이 같으면
    Discount, // 하나로 축약 가능함
    Modal,
    Card,
  },
};
</script>

<style>
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