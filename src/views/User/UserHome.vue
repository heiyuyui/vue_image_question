<template>
  <div>
    <loading :active.sync="isLoading"></loading>
    <banner></banner>
    <section class="bg-dessert">
      <div class="container pt-5 pb-3 text-center">
        <div class="h3-title">
          <p class="h3">heiyuyui總是在詢問</p>
          <p class="h3">這麼好吃的秘訣是什麼</p>
        </div>
        <div class="row mt-4">
          <div class="col-md-4 d-flex align-items-center flex-column" data-aos="zoom-in">
            <div class="box box-1 mb-4"></div>
            <h3>兔兔</h3>
            <p>
              <br />嚴選最安心、自然的食材。
              <br />heiyuyui堅持不添加防腐劑及任何食品添加物
            </p>
          </div>
          <div class="col-md-4 d-flex align-items-center flex-column" data-aos="zoom-in">
            <div class="box box-2 mb-4"></div>
            <h3>鳥鳥</h3>
            <p>
              我們的餅乾是經由heiyuyui師傅
              <br />每天新鮮現做
              <br />保證一定的品質
            </p>
          </div>
          <div class="col-md-4 d-flex align-items-center flex-column" data-aos="zoom-in">
            <div class="box box-3 mb-4"></div>
            <h3>狗狗</h3>
            <p>
              有別於一般的甜點
              <br />我們發揮更多的創意於甜點的口味
              <br />創造出味蕾的饗宴
            </p>
          </div>
        </div>
      </div>
    </section>
    <section class="bg-wooden">
      <div class="container py-5" data-aos="fade-up">
        <p class="h3 text-center">熱門產品</p>
        <div class="product-wrap mx-auto">
          <swiper :options="swiperOption">
            <swiper-slide class="p-2" v-for="(item) in products" :key="item.id">
              <router-link
                class="card shadow-sm card-round text-decoration-none border-0"
                :to="{path : `/product/${item.id}` }"
              >
                <div class="pic">
                  <div :style="{backgroundImage :`url(${item.image})`}" class="pic-enlarge"></div>
                </div>
                <div class="card-body">
                  <span class="badge badge-secondary mb-2">{{ item.category }}</span>
                  <h5 class="card-title text-dark">{{ item.title }}</h5>
                </div>
              </router-link>
            </swiper-slide>
          </swiper>
          <div class="swiper-button swiper-button-left fas fa-chevron-circle-left fa-2x text-white"></div>
          <div class="swiper-button swiper-button-right fas fa-chevron-circle-right fa-2x text-white"></div>
        </div>
      </div>
    </section>
  </div>
</template>
<script>
import banner from '@/components/Banner.vue'
export default {
  data () {
    return {
      swiperOption: {
        observer: true,
        observeParents: true,
        autoplay: {
          delay: 3000
        },
        loop: true,
        speed: 1000,
        slidesPerView: 1,
        breakpoints: {
          540: {
            slidesPerView: 2
          },
          768: {
            slidesPerView: 3
          },
          992: {
            slidesPerView: 4
          }
        },
        navigation: {
          nextEl: '.swiper-button-right',
          prevEl: '.swiper-button-left'
        }
      }
    }
  },
  components: {
    banner
  },
  methods: {
    getProducts () {
      this.$store.dispatch('getProducts')
    }
  },
  computed: {
    products () {
      return this.$store.state.products
    },
    isLoading () {
      return this.$store.state.isLoading
    }
  },
  created () {
    const vm = this
    vm.getProducts()
  }
}
</script>
