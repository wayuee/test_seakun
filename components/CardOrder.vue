<template>
  <div class="div-top">
    <div v-if="showModal" @click="showModal = false"></div>
    <div @click="showModal = true">
      <div class="relative border rounded-lg mb-5 cursor-pointer">
        <h1 class="border-b p-1 pl-3">
          Order Id : {{ cardOrder.orderId }}
          <span class="span-top"
            >Create At : {{ getcardOrderYear(cardOrder.createdAt) }}</span
          >
        </h1>
        <h1 class="ml-5">Info Akun</h1>
        <div class="grid grid-cols-3 ml-5">
          <h1>{{ cardOrder.personalAccount.name }}</h1>
          <span
            class="span-mid"
            v-if="cardOrder.provider === '12387163476137846'"
            >Provider : Netflix</span
          >
          <span class="span-mid" v-else-if="cardOrder.provider === 'Netflix'"
            >Provider : Netflix</span
          >
          <span class="span-mid" v-else-if="cardOrder.provider === 'Spotify'"
            >Provider : Spotify</span
          >
        </div>
        <div class="grid grid-cols-3 ml-5">
          <h1>{{ cardOrder.personalAccount.email }}</h1>
          <span class="span-mid" v-if="cardOrder.paket === 'Paket Netflix'"
            >Paket : Paket Netflix</span
          >
          <span class="span-mid" v-if="cardOrder.paket === 'Paket Spotify'"
            >Paket : Paket Spotify</span
          >
          <span class="span-mid" v-if="cardOrder.paket === 'Paket sppotify'"
            >Paket : Paket Spotify</span
          >
          <span class="span-price"
            >Rp {{ formatPrice(cardOrder.payment.paymentTotal) }}</span
          >
        </div>
        <div class="grid grid-cols-3 ml-5">
          <h1>{{ cardOrder.personalAccount.phonenumber }}</h1>
          <span class="span-bottom"
            >Exp {{ getcardOrderYear(cardOrder.expired) }}</span
          >
        </div>
      </div>
    </div>

    <div id="app">
      <div class="modal" v-if="showModal">
        <div class="pt-5 pl-7 text-2xl">Order Detail</div>
        <div class="border rounded-xl mt-10 mx-7">
          <h1 class="border-b p-1 pl-3">
            Order Id : {{ cardOrder.orderId }}
            <span class="span-top"
              >Create At : {{ getcardOrderYear(cardOrder.createdAt) }}</span
            >
          </h1>
          <h1 class="ml-5">Info Akun</h1>
          <div class="grid grid-cols-3 ml-5">
            <h1>{{ cardOrder.personalAccount.name }}</h1>
            <span
              class="span-mid"
              v-if="cardOrder.provider === '12387163476137846'"
              >Provider : Netflix</span
            >
            <span class="span-mid" v-else-if="cardOrder.provider === 'Netflix'"
              >Provider : Netflix</span
            >
            <span class="span-mid" v-else-if="cardOrder.provider === 'Spotify'"
              >Provider : Spotify</span
            >
          </div>
          <div class="grid grid-cols-3 ml-5">
            <h1>{{ cardOrder.personalAccount.email }}</h1>
            <span class="span-mid" v-if="cardOrder.paket === 'Paket Netflix'"
              >Paket : Paket Netflix</span
            >
            <span class="span-mid" v-if="cardOrder.paket === 'Paket Spotify'"
              >Paket : Paket Spotify</span
            >
            <span class="span-mid" v-if="cardOrder.paket === 'Paket sppotify'"
              >Paket : Paket Spotify</span
            >
            <span class="span-price"
              >Rp {{ formatPrice(cardOrder.payment.paymentTotal) }}</span
            >
          </div>
          <div class="grid grid-cols-3 ml-5">
            <h1>{{ cardOrder.personalAccount.phonenumber }}</h1>
            <span class="span-bottom"
              >Exp {{ getcardOrderYear(cardOrder.expired) }}</span
            >
          </div>
        </div>
        <div class="border rounded-xl mt-5 mx-7 p-5">
          <h4>Voucher Code : {{ cardOrder.voucherCode }}</h4>
          <h4>Payment Status : {{ cardOrder.payment.status }}</h4>
          <h4>
            Payment Date : {{ getcardOrderYear(cardOrder.payment.paymentDate) }}
          </h4>
          <h4>Payment Bank : {{ cardOrder.payment.name }}</h4>
        </div>
        <button class="button-close" @click="showModal = false">
          Close Modal
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showModal: false,
    };
  },
  props: {
    cardOrder: {
      type: Object,
      default: () => [],
    },
  },
  methods: {
    formatPrice(value) {
      let val = (value / 1).toFixed(0).replace(".");
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    },
    getcardOrderYear(value) {
      const getDate = new Date(value.slice(0, 10)).toDateString();
      return getDate.slice(3, 15);
    },
  },
};
</script>

<style>
.div-top {
  padding: 20px 0;
}
#app {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.button {
  cursor: pointer;
  position: absolute;
  padding: 3px 10px;
  right: 50px;
  top: 125px;
  background-image: linear-gradient(to right, #462ecc, #589bff);
  border-radius: 10px;
  color: #fff;
}

.button-close {
  cursor: pointer;
  padding: 2px 10px;
  background-image: linear-gradient(to right, #462ecc, #589bff);
  border-radius: 8px;
  float: right;
  color: #fff;
  margin: 25px 20px;
  transition: 0.4s ease-out;
}

.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 99;
  border: 1px solid black;
  width: 100%;
  max-width: 1000px;
  background-color: #fff;
  border-radius: 16px;
  box-shadow: 20rem 20rem 20rem 50rem rgba(0, 0, 0, 0.452);
}

.span-mid {
  border-left: 2px solid rgb(146, 139, 139);
  padding: 1.5px 0;
}
.span-top {
  float: right;
  margin-right: 30px;
}
.span-bottom {
  margin-bottom: 20px;
  border-left: 2px solid rgb(146, 139, 139);
}
.span-price {
  font-size: 25px;
  margin-bottom: -10px;
}
</style>
