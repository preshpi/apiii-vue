<template>
  
  <div class="bg-gray-900 body ">
  <h1 class="text-3xl text-center  text-bold text-white font-serif p-5">Miami Store</h1>
  <p class="text-center text-xl text-blue-600 italic">Check out our latest products...</p>

  <div class="mb-3 pt-0 text-center justify-center mt-8">
  <input type="text" v-model="search" placeholder="Search a product..." class="px-5 py-3 placeholder-slate-300  bg-white rounded text-sm border-0 shadow outline-none focus:outline-none focus:ring w-60 text-black"/>
  </div> 

                <!-- Main -->
     <div class="grid lg:grid-cols-3 md:grid-cols-2 p-8 justify-center">
      <div v-for="item in filteredItems" v-bind:key="item.id" class="m-3">
        <div class="max-w-sm rounded overflow-hidden shadow-lg">
        <img class="w-full images" :src="item.thumbnail" alt="Sunset">

          <div class="px-6 py-4 bg-gray-50">
            <div class="flex justify-between">
            <div class="font-bold text-xl">{{item.title}}</div>
            <span class=" text-xl font-bold text-gray-700 mr-2 ">${{item.price}}</span>
            </div>
            <p class="font-bold text-xl mb-2 mt-2 font-italic">{{item.brand}}</p>
            <p class="font-bold text-xl mb-2 mt-2 font-italic">{{item.category}}</p>
            <p class="text-gray-700 text-base desc">{{item.description}}</p> 
            <!-- <p class="text-center text-black text-x font-mono mt-3">More products</p> -->
   
            <div v-for="item in item.image" v-bind:key="item.id">
              <img :src="image.image"/>
            </div>

              <div class=" flex justify-between mt-3">
              <span class="font-semibold text-sm mr-2 mb-2 text-red-500 text-right">Discount: {{item.discountPercentage}}%</span>
              <span class="text-sm font-semibold text-gray-700 mr-2 mb-2 text-left">Rating: {{item.rating}}</span>           
            </div>

        </div>
      </div> 

      </div>
    </div>

   
         <!-- footer -->
         <div class="bg-gray-200 text-center lg:text-left">
          <div class="text-gray-700 text-center p-4">
           <p>Made with &#128151; by Precious</p>
          </div>
        </div>

  </div>
  
</template>

<script>
  import HelloWorld from '@/components/HelloWorld.vue'
  import Vue from 'vue';
  import axios from 'axios';
  import VueAxios from 'vue-axios';
  Vue.use(VueAxios,axios)
export default {
  name: 'HomeView',
  components: {
    HelloWorld
  },
  data()
  {
  return{
    list: [],
    images: [],
    search:''
  }
    
  },
  mounted()
  {
    Vue.axios.get('https://dummyjson.com/products')
    .then((resp)=> {
      this.list=resp.data.products;
      console.warn(resp.data.products)
    })

  },
  computed: {
    filteredItems: function(){
      return this.list.filter((item) => {
        return item.title.toLowerCase().includes(this.search.toLowerCase())
      })
    }
  }


}
</script>

<style>
.body{
font-family: 'Inter', sans-serif;
font-family: 'Lato', sans-serif;    
}

img{
  width:70%;
}
.images{
  width: 100px;
  height: 250px;
  object-fit: cover;
}

.desc{
  position: relative;
  max-height: 50px;
  overflow: hidden;
  padding-right: 0.6rem;
  font-size: 0.8rem;
  color: #a9a9a9;
}

.desc::before{
  position: absolute;
  content: '...';
  bottom: 0;
  right: 0;
}
</style>


