<template>

  <div class="menu">
    <!-- <a>Home</a>
    <a>Products</a>
    <a>About</a> -->

    <!--
      반복문 <v-for="변수명 in 몇회/데이터배열" :key="변수명">{{ 변수명 }}
      for문 변수 작명은 2개까지 가능. v-for="(변수명, i) in 배열"
      왼쪽 변수는 배열의 데이터, 오른쪽 변수는 1씩 증가하는 정수
      :key="" 는 반복문 쓸 때 꼭 써야함. 반복문 돌린 요소를 컴퓨터가 구분하기 위해 필요함
    -->
    <a v-for="i in menu" :key="i">{{ i }}</a>
  </div>

  <!-- <div>
    <h4 class="red" :style="스타일">{{ products[0] }}</h4>
    <p>{{ price1 }} 만원</p>
  </div>
  <div>
    <h4>{{ products[1] }}</h4>
    <p>{{ price2 }} 만원</p>
  </div>
  <div>
    <h4>{{ products[2] }}</h4>
    <p>{{ price3 }} 만원</p>
  </div> -->
  <div v-for="(data, i) in products" :key="i">
    <h4>{{ products[i] }}</h4>
    <p>{{ price[i] }} 만원</p>
  </div>
</template>

<script>
// var products = ['역삼동 원룸', '천호동 원룸', '마포구 원룸'];

export default {
  name: "App",
  data() {
    // 데이터 보관함. object 형식으로 중요 변수들을 담아두면 됨
    // template 에서 데이터 바인딩 -> 실시간 자동렌더링
    return {
      // price1: 60,
      // price2: 150,
      // price3: 80,
      price: [60, 150, 80],
      products: ['역삼동 원룸', '천호동 원룸', '마포구 원룸'],
      // html 속성 안에서 바인딩 할 때는 <:속성="데이터 키값">
      스타일: 'color: blue',
      menu: ['Home', 'Products', 'About']
    };
  },
  components: {},
};
</script>

<style>
.menu {
  background-color: darkslateblue;
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
