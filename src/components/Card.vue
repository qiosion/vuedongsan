<template>
<!-- 
  props 쓰는 법
    1. 부모 컴포넌트에서 v-bind: 또는 : 를 사용하여 보내고싶은 데이터 전송 
        :변수명="전송하고자 하는 데이터(아래에서 설정한 값)"
        colon 은 속성에 데이터 바인딩할 때, props 전송할 때 사용
    2. 자식 컴포넌트에서 default 값에 props 등록
        json 형태로 등록, {데이터 이름: 자료형 이름}
  
  $emit()
    props 는 read-only. 자식 컴포넌트에서 수정하면 에러 발생.
    이때 custom event 로 자식이 메시지 전송하여 해결
      자식 -> 부모 메시지 전송 :$emit('변수명') 또는  $emit('변수명', 데이터)
      부모가 메시지 수신 : @변수명="해당 변수명을 수신했을 때 실행할 js 코드"
                        이때 js 코드 안에서 $event 를 사용하여 받은 데이터를 사용 가능
    $emit() 을 함수 안에 쓰고싶다면 this.$emit()
-->
  <div>
    <img class="room-img" :src="oneroom.image">
    <!-- <h4 @click="$emit('openModal', oneroom.id)">{{ oneroom.title }}</h4> -->
    <h4 @click="openFunction">{{ oneroom.title }}</h4>
    <p>{{ oneroom.price }} 원</p>
  </div>
</template>
<script>
export default {
  name: 'Card',
  props: {
    oneroom: Object,
  },
  methods: {
    openFunction() {
      this.$emit('openModal', this.oneroom.id)
    }
  }
}
</script>