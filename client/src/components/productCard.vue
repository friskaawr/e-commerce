<template>
  <div class="card-item">
    <b-card no-body img-alt="Image" img-top class="card-body" @click="detailItem(product._id)">
      <img
        v-if="!product.image"
        src="https://wanowi.com/public/uploads/products/list/product-default.jpg"
        alt="user"
        height="200"
        style="display:block; margin:auto;"
      />
      <img
        v-if="product.image"
        :src="product.image"
        alt="productpicture"
        width="200"
        height="200"
        style="display:block; margin:auto;"
      />
      <!-- <img v-if="product.image" :src="product.image" alt="picture">
      <img v-if="!product.image"
        src="data:image/png;base64,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"
        alt="productpicture"
        width="200"
        height="200"
        style="display:block; margin:auto;"
        class="product-image"
      />-->
      <b-card-body>
        <b-card-title>{{product.productname}}</b-card-title>
        <b-card-sub-title class="mb-2">Total : {{product.qty}}</b-card-sub-title>
        <b-card-text>{{convertIdr(product.price)}}</b-card-text>
      </b-card-body>
      <button @click="addtoCart(product._id)" class="button-cart">Add to Cart</button>
    </b-card>
  </div>
</template>

<script>
import axios from "../config/axios.js";

export default {
  props: ["product"],
  data() {
    return {
      products: {}
    };
  },
  methods: {
    addtoCart(id) {
      if (!localStorage.getItem("token")) {
        this.$router.push("/login");
      } else {
        console.log("masuk sini");

        axios({
          method: "POST",
          url: "/carts/add",
          data: {
            ProductId: id,
            quantity: 1
          },
          headers: { token: localStorage.getItem("token") }
        })
          .then(({ data }) => {
            Swal.fire(
              'Success!',
              'This item already in your cart!',
              'success'
            )
          })
          .catch(err => {
            Swal.fire({
              type: "error",
              title: "Oops...",
              text: "Something went wrong!"
            })
            console.log(err);
          })
      }
    },
    convertIdr(price) {
      let str = String(price);
      let convert = [];
      let dlm = "";
      for (let i = str.length - 1; i >= 0; i--) {
        dlm = str[i] + dlm;

        if (dlm.length == 3 || i == 0) {
          // console.log("masuk");
          convert.push(dlm);
          dlm = "";
        }
      }
      return `Rp ${convert.reverse().join(".")},-`;
    },
    detailItem(id) {
      this.$router.push(`/products/${id}`);
    }
  },
  created() {
    this.products;
  }
};
</script>

<style scoped>
.card-item {
  width: 250px;
  margin-bottom: 30px;
}
.button-cart {
  border: none;
  height: 40px;
  width: 200px;
  border-radius: 3%;
  background-color: #fcca46;
}

.button-cart:hover {
  background-color: #d8572a;
  color: #fff;
}
/*.card-body:hover + .button-cart{
        display: inline-block;
    } */
</style>
