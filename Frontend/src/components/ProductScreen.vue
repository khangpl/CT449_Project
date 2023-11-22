<template>
   <div class="row">
      <div id="content" class="col-sm-12">
         <div class="header-content">
            <h3 class="title">Truyện Tranh - Manga</h3>
            <form class="form-inline my-2 my-lg-0 search-btn">
               <input
                  class="form-control mr-sm-2"
                  type="search"
                  placeholder="Tìm kiếm..."
                  aria-label="Search"
                  v-model="searchText"
               />
               <button
                  class="btn btn-outline-success my-2 my-sm-0"
                  type="submit"
               >
                  <i class="fas fa-search"></i>
               </button>
            </form>
         </div>
         <div class="row product-category">
            <div v-if="filteredProductsCount > 0"></div>
            <p class="non-product" v-else>Không có sản phẩm nào</p>
            <div
               class="product-grid col-lg-3"
               :key="index"
               v-for="(product, index) in filteredProducts"
            >
               <div class="thumb">
                  <div class="image">
                     <a href="#"
                        ><img :src="product.imgUrl" alt="Sản phẩm"
                     /></a>
                  </div>
                  <div class="caption">
                     <h4>
                        <a href="#" class="product-name">
                           {{ product.name }}
                           
                           <!-- {{ product.description }} -->
                        </a>
                     </h4>
                     <p class="price">
                        {{
                           product.price.replace(/\B(?=(\d{3})+(?!\d))/g, ".")
                        }}
                        đồng
                     </p>
                  </div>
                  <div class="botton-cart">
                     <button class="btn-cart" @click="addProductToCart(index)">
                        Thêm vào giỏ
                     </button>
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
</template>

<script>
import ProductService from "../services/product.service";

export default {
   data() {
      return {
         products: [],
         searchText: "",
      };
   },

   computed: {
      productStrings() {
         return this.products.map((product) => {
            const { name, description } = product;
            return [name, description].join("");
         });
      },
      filteredProducts() {
         if (!this.searchText) return this.products;
         return this.products.filter((_product, index) =>
            this.productStrings[index].includes(this.searchText)
         );
      },
      filteredProductsCount() {
         return this.filteredProducts.length;
      },
   },
   methods: {
      async getAllProduct() {
         try {
            this.products = await ProductService.getAll();
         } catch (error) {
            console.log(error);
         }
      },
      async addProductToCart(index) {
         const saveLocalCart = JSON.parse(
            localStorage.getItem("localProductCart") ?? "[]"
         );
         for (const item of saveLocalCart) {
            if (item.id === this.products[index]._id) {
               item.amount++;
               const localProductCart = JSON.stringify(saveLocalCart);
               localStorage.setItem("localProductCart", localProductCart);
               alert(
                  `Số lượng sản phẩm ${this.products[index].name} đã được cập nhật`
               );
               return;
            }
         }
         const temp = {
            id: this.products[index]._id,
            name: this.products[index].name,
            imgUrl: this.products[index].imgUrl,
            price: this.products[index].price,
            description: this.products[index].description,
            amount: 1,
         };
         saveLocalCart.push(temp);
         const localProductCart = JSON.stringify(saveLocalCart);
         localStorage.setItem("localProductCart", localProductCart);
         alert(
            `Sản phẩm ${this.products[index].name} vừa được thêm vào giỏ hàng`
         );
      },
   },

   created() {
      this.getAllProduct();
   },
};
</script>

<style scoped>
@font-face {
   font-family: 'nunito';
   src: url(./src/fonts/Nunito/Nunito-Italic-VariableFont_wght.ttf) format('truetype');
   font-style: normal;
   font-weight: normal;
 }

.row {
   padding-top: 30px;
}
#content {
   min-height: 400x;
}
.product-category {
   padding-top: 0px;
}
.header-content {
   display: flex;
   border-bottom: 3px solid #eee;
   font-family: 'Nunito';
   font-weight: normal;
   font-size: 22px;
}
.search-btn {
   padding-left: 338.5px;
   padding-bottom: 20px;
}
.non-product {
   margin-left: 450px;
   margin-top: 15px;
   font-size: 20px;
   font-weight: bold;
   color: rgb(1, 1, 2);
   margin: 0 auto;
}
.product-grid {
   height: 300px;
   position: relative;
   text-align: center;
   vertical-align: top;
   padding: 7px;
   margin-bottom: 15px;
   border: 3px solid transparent;
}
.product-grid:hover {
   border-color: #eae9e9;
}
.product-grid .thumb img {
   object-fit: cover;
   height: 150px;
}
.product-grid .thumb .caption h4 a {
   font-size: 13px;
   line-height: 22px;
   text-decoration: none;
   padding: 5px;
   color: #333;
   margin: 0 auto;
   width: 100%;
   overflow: hidden;
   text-overflow: ellipsis;
   -webkit-line-clamp: 2;
   display: -webkit-box;
   -webkit-box-orient: vertical;
}
.price {
   color: #ff0000;
   font-weight: bold;
}
.btn-primary {
   background-color: #3e7cb4;
}
.botton-cart {
   position: absolute;
   bottom: 0;
   left: calc(50% - 55px);
}
.btn-cart {
   background-color: #3e7cb4;
   color: #fff;
   border-radius: 3px;
}
.btn-cart:hover {
   background-color: #1760a0;
}
</style>
