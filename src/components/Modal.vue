<template>
  <div v-if="modal_status" class="black-bg">
    <div class="white-bg">
      <h4>{{ modalRoom.title }}</h4>
      <p>{{ modalRoom.content }}</p>
      <input v-model.number="month">
      <p>{{ month }}개월 가격 {{ month * modalRoom.price }}원</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Modal',
  props: {
    modal_status : Boolean,
    modalRoom : Object
  },
  data() {
    return {
      month : 1
    }
  },
  watch : {
    month(input, result) {
      if (isNaN(input)) {
        alert("잘못된 입력");
        this.month = result;
      }
      if (input > 12) {
        alert("13이상 입력 X");
        this.month = result;
      }
    }
  },
  updated() {
    if (this.month === 2) {
      alert("2 업데이트");
    }
  }
}
</script>

<style>

</style>