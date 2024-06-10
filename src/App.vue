<template>
  <div class="menu">
    <a v-for="i in menu" :key="i">{{ i }}</a>
  </div>

<!-- 컴포넌트로 빼기 전
  <div class="discount">
    <h4>지금 결제 시 20% 할인</h4>
  </div>

  컴포넌트 쓰는 법
    1. .vue 파일을 생성하여 코드 작성
    2. script에서 vue 파일을 import
    3. export 하는 곳의 components 에 등록
  
  컴포넌트 사용은 재사용하는 경우에만 사용하자! 무조건 빼지 말고.
  데이터 바인딩 한 것은 컴포넌트로 빼면 못씀.
  따라서 보통 데이터는 한곳(부모컴포넌트)에 집어넣어서 갖다씀(props)
  자식에서만 쓰면 처음부터 데이터를 자식에 만들면 되는데, 아니면 최상위에 쓰고 props로 전송

  Object 자료형만 v-bind 를 사용해서 한번에 보낼 수 있음
-->
  <Discount v-bind="Object" />
  <!-- <Discount :name="Object.name" :age="Object.age" /> -->

<!-- 
  props 쓰는 법
    1. 부모 컴포넌트에서 v-bind: 또는 : 를 사용하여 보내고싶은 데이터 전송 
        :변수명="전송하고자 하는 데이터(아래에서 설정한 값)"
        colon 은 속성에 데이터 바인딩할 때, props 전송할 때 사용
    2. 자식 컴포넌트에서 default 값에 props 등록
        json 형태로 등록, {데이터 이름: 자료형 이름}
    
  props 는 read-only. 자식 컴포넌트에서 수정하면 에러 발생
 -->
  <Modal :onerooms="onerooms" :clicked="clicked" :isModalOpen="isModalOpen" />

  <Card v-for="(oneroom, i) in onerooms"
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