## vue-awesome-swiper

官网链接https://www.npmjs.com/package/vue-awesome-swiper

1. **下载npm包**

   > `npm install vue-awesome-swiper --save `

2. **vue组件中使用**

   模板中：

   ```vue
   <template>
     <swiper :options="swiperOption" ref="mySwiper">
       <!-- slides -->
       <swiper-slide>I'm Slide 1</swiper-slide>
       <swiper-slide>I'm Slide 2</swiper-slide>
       <swiper-slide>I'm Slide 3</swiper-slide>
       <swiper-slide>I'm Slide 4</swiper-slide>
       <swiper-slide>I'm Slide 5</swiper-slide>
       <swiper-slide>I'm Slide 6</swiper-slide>
       <swiper-slide>I'm Slide 7</swiper-slide>
       <!-- Optional controls -->
       <div class="swiper-pagination"  slot="pagination"></div>//
       <div class="swiper-button-prev" slot="button-prev"></div>
       <div class="swiper-button-next" slot="button-next"></div>
       <div class="swiper-scrollbar"   slot="scrollbar"></div>
     </swiper>
   </template>
   ```

   

   script中：

   ```vue
   <script>
   import 'swiper/dist/css/swiper.css'
   import { swiper, swiperSlide } from 'vue-awesome-swiper'
   export default {
     components: {
       swiper,
       swiperSlide
     },
     data() {
       return {
         swiperOption: {}
       };
     },
     computed: {
       swiper() {
         return this.$refs.mySwiper.swiper;
       }
     },
   }
   </script>
   ```

   
