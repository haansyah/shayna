<template>
  <div class="product">
    <HeaderShayna />
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="breadcrumb-text product-more text-left" >
                        <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
                        <span>Detail</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="row">
                        <div class="col-lg-6">
                            <div class="product-pic-zoom">
                                <img class="product-big-img" :src="gambar_default" alt="" />
                            </div>
                            <div class="product-thumbs" v-if="productDetails.galleries.length > 0">
                                <carousel :dots="false" :nav="false" class="product-thumbs-track ps-slider">
                                    <div
                                    v-for="ss in productDetails.galleries"
                                    :key="ss.id"
                                    class="pt"
                                    @click="changeImage(ss.photo)"
                                    :class="ss.photo == gambar_default ? 'active' : '' "
                                    >
                                    <img :src="ss.photo" alt />
                                    </div>
                                </carousel>
                            </div>
                        </div>
                        <div class="col-lg-6">
                            <div class="product-details text-left">
                                <div class="pd-title">
                                    <span>{{ productDetails.type }}</span>
                                    <h3>{{ productDetails.name }}</h3>
                                </div>
                                <div class="pd-desc">
                                    <p>
                                        {{ productDetails.description }}
                                    </p>
                                    <h4>${{ productDetails.price }}</h4>
                                </div>
                                <div class="quantity">
                                    <router-link to="/cart"><a href="shopping-cart.html" class="primary-btn pd-cart">Add To Cart</a></router-link>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Product Shop Section End -->
    <RelatedShayna/>
    <FooterShayna />
  </div>

</template>

<script>
import HeaderShayna from '@/components/HeaderShayna.vue';
import FooterShayna from '@/components/FooterShayna.vue';
import RelatedShayna from '@/components/RelatedShayna.vue';

import carousel from 'vue-owl-carousel';

import axios from "axios";


export default {
  name: 'Product',
  components: {
    HeaderShayna,
    RelatedShayna,
    FooterShayna,
    carousel
  },
  data() {
      return{
          gambar_default: '',
          thumbs: [
              "img/mickey1.jpg",
              "img/mickey2.jpg",
              "img/mickey3.jpg",
              "img/mickey4.jpg"
          ],
          productDetails: []
      }
  },
  methods: {
      changeImage(urlImage) {
          this.gambar_default = urlImage;
      },
    setDataPicture(data) {
        // replace object productDetails dengan data dari API
        this.productDetails = data;
        // replace value gambar default dengan data dari API (galleries)
        this.gambar_default = data.galleries[0].photo;
    },
  },
  mounted() {
        axios
            .get("http://127.0.0.1:8000/api/products", {
                params: {
                    id: this.$route.params.id
                }
            })
            .then(res => (this.setDataPicture(res.data.data)))
            // eslint-disable-next-line no-console
            .catch(err => console.log(err));
    }
}
</script>

<style scoped>
.product-thumbs .pt {
    margin-right: 14px;
}
</style>