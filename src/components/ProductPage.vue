<template>
  <div class="page">
    <div class="result">
      <router-link to="/">
        <span class="fa fa-angle-left"> Back to Home</span></router-link
      >
    </div>
    <div class="row">
      <div class="Image1">
        <div class="image">
          <img
            :src="product.thumbnail"
            alt="Image"
            class="Image"
            height="400px"
            width="600px"
          />
        </div>
      </div>
      <div class="data">
        <div class="product-info">
          <div class="product-title">{{ product.title }}</div>
          <p class="product-rating">
            {{ product.rating }}
            <span class="fa fa-star checked"></span>/ 5 -
            <span class="fa fa-check">people's choice</span>
          </p>
          <div class="product-price">${{ product.price }}.00</div>
          <div class="heading">About Item</div>
          <div class="product-description">
            <ul>
              <li>
                {{ product.description }}
              </li>
            </ul>
          </div>
          <table class="features">
            <tr class="category">
              <th>Brand</th>
              <td>{{ product.brand }}</td>
            </tr>
            <tr class="category">
              <th>Category</th>
              <td>{{ product.category }}</td>
            </tr>
            <tr class="category">
              <th>discount Percentage on product</th>
              <td>{{ product.discountPercentage }}</td>
            </tr>
          </table>
          <div class="product-actions">
            <button class="btn" @click="gotocart">Add to Cart</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["id"],
  data() {
    return {
      product: {},
    };
  },
  created() {
    // console.log(this.id);
    axios
      .get("https://dummyjson.com/products/" + this.id)
      .then((response) => {
        // console.log(response);
        this.product = response.data;
        // console.log(this.product);
      })
      .catch((error) => {
        console.log(error);
      });
  },
  methods: {
    gotocart() {
      this.$store.commit("addToCart", this.product);
      this.$router.push({
        name: "Cart",
      });
    },
  },
};
</script>

<style scoped>
.checked {
  color: orange;
}
.result {
  text-align: left;
  background: whitesmoke;
}

.page {
  height: 100vh;
}
.row {
  margin-top: 15px;
  padding: 50px;
  display: flex;
  justify-content: space-evenly;
}

.fa-check {
  color: green;
}

.data {
  /* width: 60%; */
  align-content: left;
  text-align: left;
}

.btn {
  border: none;
  height: 30px;
  width: 100px;
  margin-left: 60px;
  color: #fff;
  background: orange;
}

.product-title {
  font-size: 20px;
  font-weight: bold;
  margin-left: 50px;
}

.product-rating,
.product-price,
.product-description,
.heading {
  margin-bottom: 10px;
  margin-left: 50px;
}
ul {
  list-style-position: outside;
}

.product-price {
  color: #b12704;
}
.heading {
  font-size: 20px;
  font-weight: bold;
}

.product-title {
  font-size: 30px;
  text-transform: capitalize;
}

.features {
  border: 1px solid #000;
  margin-top: 50px;
  margin-left: 50px;
  margin-bottom: 30px;
}

th,
td {
  padding: 5px;
  border: 1px solid #000;
}
</style>
