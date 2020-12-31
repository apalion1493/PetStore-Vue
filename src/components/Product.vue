<template>
  <div>
    <my-header></my-header>
    <div class="container">
      <h1>This is the ID {{$route.params.id}}</h1>
      <div class="row">
        <div class="col-md-5">
          <figure>
            <img v-bind:src="product.image" alt="" class="product">
          </figure>
        </div>
        <div class="col-md-6 description">
          <h1>{{product.title}}</h1>
          <p class="price">{{product.price}}</p>
          <button class="btn btn-primary" @click="edit">Edit Product</button>
          <router-view></router-view>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import MyHeader from "@/components/Header";
export default {
  components: {MyHeader},
  data() {
    return {
      product: '',
      baseUrl: process.env.VUE_APP_BASE_URL,
    }
  },
  created: function () {
    this.axios.get(this.baseUrl + 'products.json').then(response => {
      this.product = response.data.products.filter(
          data => data.id == this.$route.params.id)[0]
      this.product.image = '/' + this.product.image
    });
  },
  methods: {
    edit() {
      this.$router.push({name: 'Edit'})
    }
  }
}
</script>
