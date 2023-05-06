<template>
  <div class="product">
    <div v-if="isLoading" class="position">
      <div class="loader"></div>
    </div>
    <div class="product__card">
      <div
        class="product__cart-no-avaible"
        :class="
          isProductAvailable ? 'display-none' : 'product__cart-no-avaible'
        "
      >
        <p class="text-no">This product is unavailable to show</p>
        <button class="btn__no-avaible" @click="getSingleProduct()">
          Next product
        </button>
      </div>
      <div
        class="product__card-avaible"
        :class="!isProductAvailable ? 'display-none' : 'product__card-avaible'"
      >
        <div class="product__right-side">
          <!-- <img src="../components/img.png" alt="Image Men" class="product__img" /> -->
          <img :src="product?.data?.image" alt="" class="product__img" />
        </div>
        <div class="product__left-side">
          <h1
            :class="
              product?.data?.category === 'men\'s clothing'
                ? 'font-navy'
                : 'font-magenta'
            "
            class="product__name"
          >
            {{ product?.data?.title }}
          </h1>
          <div class="product__information">
            <h4 class="product__genre">{{ product?.data?.category }}</h4>
            <div class="product__ratings">
              <p class="product__rating-number">
                {{ product?.data?.rating?.rate }}/5
              </p>
              <div class="product__rating-circle">
                <div
                  class="circle"
                  :class="
                    product?.data?.category === 'men\'s clothing'
                      ? 'bg-navy'
                      : 'bg-magenta'
                  "
                ></div>
                <div
                  class="circle"
                  :class="
                    product?.data?.category === 'men\'s clothing'
                      ? 'bg-navy'
                      : 'bg-magenta'
                  "
                ></div>
                <div
                  class="circle"
                  :class="
                    product?.data?.category === 'men\'s clothing'
                      ? 'bg-navy'
                      : 'bg-magenta'
                  "
                ></div>
                <div
                  class="circle"
                  :class="
                    product?.data?.category === 'men\'s clothing'
                      ? 'bg-navy'
                      : 'bg-magenta'
                  "
                ></div>
                <div
                  class="circle"
                  :class="
                    product?.data?.category === 'men\'s clothing'
                      ? 'bg-navy'
                      : 'bg-magenta'
                  "
                ></div>
              </div>
            </div>
          </div>
          <p
            class="product__description"
            :class="
              product?.data?.category === 'men\'s clothing'
                ? 'font-navy'
                : 'font-magenta'
            "
          >
            {{ product?.data?.description }}
          </p>
          <p
            class="product__price"
            :class="
              product?.data?.category === 'men\'s clothing'
                ? 'font-navy'
                : 'font-magenta'
            "
          >
            ${{ product?.data?.price }}
          </p>

          <div class="btn__container">
            <button
              class="btn"
              :class="
                product?.data?.category === 'men\'s clothing'
                  ? 'bg-navy'
                  : 'bg-magenta'
              "
            >
              Buy Now
            </button>
            <button
              @click="getSingleProduct()"
              class="btn btn-outline"
              :class="
                product?.data?.category === 'men\'s clothing'
                  ? 'border-navy font-navy'
                  : 'border-magenta font-magenta'
              "
            >
              Next Product
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductDisplay",
  data() {
    return {
      isLoading: false,
      index: 0,
      isProductAvailable: false,
      product: {},
    };
  },
  methods: {
    async callAPI() {
      const response = await fetch(
        `https://fakestoreapi.com/products/${this.index}`
      );
      const result = await response.json();
      return result;
    },
    async getSingleProduct() {
      this.isLoading = true;

      if (this.index <= 20) {
        this.index++;
      } else {
        this.index = 1;
      }

      let data = await this.callAPI();
      if (
        data.category === "men's clothing" ||
        data.category === "women's clothing"
      ) {
        this.product = { data };
        this.isProductAvailable = true;
      } else {
        this.isProductAvailable = false;
      }

      this.isLoading = false;
    },
  },
  mounted() {
    this.getSingleProduct();
  },
};
</script>

<style scoped>
@import "../assets/style/page.css";
</style>
