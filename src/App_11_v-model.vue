<template>
  <div class="menu">
    <a v-for="i in menu" :key="i">{{ i }}</a>
  </div>

  <Discount v-bind="Object" />

  <Modal :onerooms="onerooms" :clicked="clicked" :isModalOpen="isModalOpen"
  @closeModal="isModalOpen = false"/>

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