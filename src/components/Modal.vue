<template>
  <div class="black-bg" v-if="isModalOpen == true">
    <div class="white-bg">
      <h4>{{ onerooms[clicked].title }}</h4>
      <img class="room-img" :src="onerooms[clicked].image">
      <p>{{ onerooms[clicked].content }}</p>
<!--
    $event : 이벤트리스너
        $event.target : 현재 이벤트가 발생하고 있는 요소(element)
        <input @input="month = $event.target.value" type="number">
    v-model : 이벤트 리스너로 js 코드작성하면 너무 길어. 축약함.
        여기 작성한 값을 아래 data에 지정한 변수에 넣어줌
    
    input : 사용자가 숫자를 입력해도 전무 문자 자료형으로 저장됨
        <input v-model="month"> 개월
    
-->
      <select v-model="month" style="width: 50px;">
        <option>12</option>
        <option>24</option>
      </select> 개월
      <p>{{ month }} 개월 당 {{ onerooms[clicked].price * month }} 원</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  data() {
    return {
      month: 1,
    }
  },
  props: {
    // 가져온 데이터 명: 타입(틀려도 됨)
    onerooms: Array,
    clicked: Number,
    isModalOpen: Boolean,
  }
}
</script>