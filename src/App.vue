<template>
  <div id="app">

    <transition name="fade">
      <Modal @closeModal="modalClose" :modalRoom="modalRoom" :modal_status="modal_status"/>
    </transition>

    <div class="menu">
      <a v-for="menu in menus" :key="menu">{{ menu }}</a>
    </div>

    <Discount :discount="discount"/>

    <button @click="priceSort">가격순 정렬</button>
    <button @click="initSort">초기화</button>

    <Card @openModal="modalOpen(room)" v-for="room in rooms" :key="room" :room="room"/>
  </div>
</template>

<script>
import data from './assets/data.js';
import Discount from "@/components/Discount.vue";
import Modal from "@/components/Modal.vue";
import Card from "@/components/Card.vue";

export default {
  name: 'App',
  data() {
    return {
      discount : 30,
      showDiscount : true,
      originRooms : [...data],
      obj : { name : 'Kim', age : 20 },
      modalRoom : {},
      rooms : data,
      modal_status : false,
      menus : [ 'Home', 'Shop', 'About' ],
      products : [{
        img : './assets/room0.jpg',
        name : '역삼동원룸',
        price : 50,
        count : 0
      }, {
        img : './assets/room1.jpg',
        name : '천호동원룸',
        price : 60,
        count : 0
      }, {
        img : './assets/room2.jpg',
        name : '마포구원룸',
        price : 70,
        count : 0
      }]
    }
  },
  methods : {
    increase(product) {
      product.count++;
    },
    modalOpen(room) {
      this.modalRoom = room;
      this.modal_status = true;
    },
    modalClose() {
      this.modal_status = false;
    },
    priceSort() {
      this.rooms.sort(function (a, b) {
        return a.price - b.price;
      })
    },
    initSort() {
      this.rooms = [...this.originRooms];
    }
  },
  mounted() {
    setInterval(() => {
      this.discount--;
    }, 1000);
  },
  components: {
    Discount : Discount,
    Modal : Modal,
    Card : Card,
  }
}
</script>

<style>
.fade-enter-from {
  opacity: 0;
}

.fade-enter-active {
  transition: all 1s;
}

.fade-enter-to {
  opacity: 1;
}

body {
  margin : 0
}

div {
  box-sizing: border-box;
}

.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 10px;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

.start {
  opacity: 0;
  transition: all 1s;
}

.end {
  opacity: 1;
}
</style>
