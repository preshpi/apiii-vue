<template>
  <div class="bg-gray-900 text-white body">
  <h1 class="text-3xl text-center p-3 text-bold">Miami Store</h1>
  <p class="text-center text-xl text-blue-600 italic">Check out our latest products...</p>
   
         <div class="grid lg:grid-cols-3 md:grid-cols-2 p-8">
             <div v-for="item in list" v-bind:key="item.id">
              <div class="m-5 text-center border border-pink-400 justify-center rounded shadow post">
              <img :src="item.thumbnail" class="images"/>
              <h3 class="text-3xl mt-2">{{item.title}}</h3>
              <p class="text-2xl mt-2">Brand: {{item.brand}}</p>
              <p class="text-xl mt-2 m-3">Description: {{item.description}}</p>  
              <div class="flex justify-around m-5">
              <p class="text-x">Category: {{item.category}}</p>
              <p class="text-x">Discount: {{item.discountPercentage}}</p>
              </div>
              <div class="flex justify-around m-5">
              <p class="text-sm">Price: ${{item.price}}</p>
              <p class="text-sm">Rating: {{item.rating}}</p>   
              </div>
              </div>
             </div>
         </div>   
         <div class="bg-gray-200 text-center lg:text-left">
          <div class="text-gray-700 text-center p-4">
           <p>Made with &#128151; by Precious</p>
          </div>
        </div>

  </div>
</template>

<script>
  import Vue from 'vue';
  import axios from 'axios';
  import VueAxios from 'vue-axios';
  Vue.use(VueAxios,axios)
export default {
  name:"Blog",
  data()
  {
    return {list:undefined}
  },
  mounted()
  {
    Vue.axios.get('https://dummyjson.com/products')
    .then((resp)=> {
      this.list=resp.data.products;
      console.warn(resp.data.products)
    })
  }

}
</script>

<style>
.body{
font-family: 'Inter', sans-serif;
font-family: 'Lato', sans-serif;    
}

.images{
  width: 100%;
  height: auto;
}


</style>