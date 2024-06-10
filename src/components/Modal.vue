<template>
  <div class="black-bg" v-if="isModalOpen == true">
    <div class="white-bg">
      <h4>{{ onerooms[clicked].title }}</h4>
      <img class="room-img" :src="onerooms[clicked].image">
      <p>{{ onerooms[clicked].price }} 원</p>
      <p>{{ onerooms[clicked].content }}</p>
      <!-- <button @click="isModalOpen = false">닫기</button> -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    // 가져온 데이터 명: 타입(틀려도 됨)
    onerooms: Array,
    clicked: Number,
    isModalOpen: Boolean,
  }
}
</script>