<template>

  <div class="menu">
    <a v-for="i in menu" :key="i">{{ i }}</a>
  </div>

  <div>
    <h4>{{ products[0] }}</h4>
    <p>{{ price1 }} 만원</p>
    <!-- v-on: == @ -->
    <button v-on:click="reportCnt[0]++">신고</button> <span>신고수 : {{ reportCnt[0] }}</span>
  </div>
  <div>
    <h4>{{ products[1] }}</h4>
    <p>{{ price2 }} 만원</p>
    <button @mouseover="reportCnt[1]++">신고</button> <span>신고수 : {{ reportCnt[1] }}</span>
  </div>
  <div>
    <h4>{{ products[2] }}</h4>
    <p>{{ price3 }} 만원</p>
    <button @mouseover="increase">신고</button> <span>신고수 : {{ reportCnt[2] }}</span>
  </div>

</template>

<script>
export default {
  name: "App",
  data() {
    return {
      price1: 60,
      price2: 150,
      price3: 80,
      products: ['역삼동 원룸', '천호동 원룸', '마포구 원룸'],
      menu: ['Home', 'Products', 'About'],
      // reportCnt: 0,
      // reportCnt2: 0,
      reportCnt: [0, 0, 0],
    };
  },
  methods: { // 함수
    increase() {
      // 함수 안에서 data의 변수를 사용하기 위해서는 this 를 붙여줌
      this.reportCnt[2] += 1;
    }
  },
  components: {},
};
</script>

<style>
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
