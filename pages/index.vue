<template>
  <div class="pb-10">
    <Navbar />
    <List />
    <div class="pl-52 pt-5 mb-7">
      <h1 class="text-2xl">Order List</h1>
      <input
        type="text"
        class="px-8 py-0.5 pl-5 border rounded-lg mb-7"
        placeholder="search name, email or orderId"
        v-model="inputSearch"
      />
      <button class="border px-5 rounded-lg mb-7" @click="buttonSearch">
        submit
      </button>
      <select
        class="float-right border cursor-pointer mr-40 pr-10"
        v-model="changeSort"
        @change="buttonSort"
      >
        <option value="" hidden>sortBy</option>
        <option value="sort">default sort</option>
        <option value="asc">ascending</option>
        <option value="desc">descending</option>
      </select>
    </div>

    <div v-for="(dataOrder, id) in paginate" :key="id">
      <OrderList :data-order="dataOrder" />
    </div>

    <div class="button-div">
      <ul>
        <li
          v-for="pageNumber in totalPages"
          v-bind:key="pageNumber.id"
          class="button-pagination"
          @click="setPage(pageNumber)"
        >
          {{ pageNumber }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Navbar from "~/components/Navbar";
import List from "~/components/List";
import OrderList from "~/components/OrderList";
export default {
  components: {
    axios,
    Navbar,
    List,
    OrderList,
  },
  data() {
    return {
      dataOrder: [],
      asc: false,
      desc: false,
      currentPage: 1,
      itemsPerPage: 5,
      resultCount: 0,
      changeSort: "",
      inputSearch: "",
      sortby: "createdAt",
    };
  },
  mounted() {
    this.getDataOrder();
  },
  methods: {
    getDataOrder() {
      let api = "https://demo2687090.mockable.io/order";
      axios
        .get(api)
        .then((res) => {
          this.dataOrder = res.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    buttonSearch() {
      this.dataOrder = this.dataOrder.filter((dataOrder) => {
        return (
          dataOrder.personalAccount.name.match(this.inputSearch) ||
          dataOrder.personalAccount.email.match(this.inputSearch) ||
          dataOrder.orderId.match(this.inputSearch) ||
          dataOrder.provider.match(this.inputSearch)
        );
      });
    },
    buttonSort() {
      return this.paginate.sort((a, b) => {
        if (this.changeSort == "asc") {
          this.asc = true;
          let dataA = a[this.sortby],
            dataB = b[this.sortby];

          if (dataA < dataB) {
            return -1;
          }
        } else if (this.changeSort == "desc") {
          this.desc = true;
          let dataA = a[this.sortby],
            dataB = b[this.sortby];

          if (dataA > dataB) {
            return -1;
          }
        } else if (this.changeSort == "sort") {
          return this.paginate;
        }
      });
    },
    setPage(pageNumber) {
      this.currentPage = pageNumber;
    },
  },
  computed: {
    totalPages() {
      if (this.resultCount == 0) {
        return 1;
      } else {
        return Math.ceil(this.resultCount / this.itemsPerPage);
      }
    },
    paginate() {
      if (!this.dataOrder) {
        return;
      }
      this.resultCount = this.dataOrder.length;
      var index = this.currentPage * this.itemsPerPage - this.itemsPerPage;
      return this.dataOrder.slice(index, index + this.itemsPerPage);
    },
  },
};
</script>

<style>
.button-div {
  margin-right: 40px;
  margin-left: 80%;
}
.button-pagination {
  cursor: pointer;
  display: inline-block;
  border: 1px solid rgb(87, 87, 87);
  background-color: lightblue;
  padding: 2px 10px;
  margin-left: 2px;
}
</style>
