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
    
    input : 사용자가 숫자를 입력해도 문자 자료형으로 저장됨

    watcher : data 감시하는 함수. 사용자의 입력을 받는 부분(input 요소)에서 꼭 필요함!
        숫자만 입력하게 하고싶은데 문자를 입력하면 경고
-->
      <input v-model="month" style="width: 40px;"> 개월
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
  watch: { // 데이터 감시. 데이터가 변할 때 마다 watch에 있는 코드가 실행됨
    // 감시할 데이터 변수명을 함수형태로 작성
    month(a) { // month (변경 후(변경 될) month 데이터, 변경 전 month 데이터) 로 파라미터 설정 가능
      if (a > 24 || a < 1) {
        alert("최소 1개월에서 최대 24개월까지 계약 가능");
        this.month = 1;
      }

      if (isNaN(a) == true) {
        alert("숫자만 입력");
        this.month = 1;
      }
    }
  },
  // hook. input 입력값이 바뀌었다면, 재렌더링 할 때(업데이트 되기 전에) 체크해서 비교
  beforeUpdate() {
    if (this.month == 2) {
      alert("3개월 부터 계약 가능");
      this.month = 3;
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