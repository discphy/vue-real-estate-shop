<template>
  <div>
    <img :src="room.image" alt="" class="room-img">
    <h4 @click="$emit('openModal', room)">{{ room.title }}</h4>
    <p>{{ room.price }}원</p>
  </div>
</template>
<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Card',
  props : {
    room : Object
  }
}
</script>

<style>

</style>