<template>
  <div class="row product-container">
    <app-product v-for="product in productList">
      <img class="card-img-top" :src="product.selectedImage" :alt="product.title">
      <div class="card-body">
        <h5 class="card-title"> {{ product.title}}</h5>
        <small>
          <strong>Number : </strong> {{ product.count }}
        </small>
        <br>
        <small>
          <strong>Price : </strong> {{ product.price }}
        </small>
        <br>
        <small>
          <strong>Total Price : </strong> {{ product.totalPrice }}
        </small>
      </div>
    </app-product>
  </div>
</template>

<script>
  import Product from "./Product";
  import { eventBus } from "../main";

  export default {
    components: {
      appProduct: Product
    },
    data() {
      return {
        productList: []
        }
      },
    created() {
      eventBus.$on("productAdded", (product) => {
        if(this.productList.length < 11) {
           this.productList.push(product);
           eventBus.$emit("progressBarUpdated", this.productList.length);
        }
        else {
          alert("Ürün eklemek için silme işlemi yapınız!");
        }
      });
    },
  }

</script>

<style scoped>

</style>