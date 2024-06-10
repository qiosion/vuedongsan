<template>
  <div class="discount">
    <h4>지금 결제 시 {{ amount }} % 할인</h4>
  </div>
</template>

<script>
export default {
  name: 'Discount',
  data() {
    return {
      amount: 10
    }
  },
  mounted() { // 마운트 되고 나서 실행
    let timer = setInterval(() => { // 지정 시간 마다 실행
      this.amount--;
      if (this.amount == 0) {
        clearInterval(timer); // 인터벌 종료
      }
    }, 1000); // 1초
  }
}
</script>

<style>

</style>