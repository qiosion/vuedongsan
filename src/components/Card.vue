<template>
  <div>
    <img class="room-img" :src="oneroom.image">
    <!-- <h4 @click="isModalOpen = true; clicked = i;">{{ onerooms[i].title }}</h4> -->
    <h4 clicked="i;">{{ oneroom.title }}</h4>
    <p>{{ oneroom.price }} 원</p>
  </div>
</template>
<script>
export default {
  name: 'Card',
  props: {
    oneroom: Object,
    isModalOpen: Boolean,
  }
}
</script>