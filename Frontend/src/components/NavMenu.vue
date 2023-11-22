<template>
   <div class="container">
      <nav class="navbar navbar-expand-lg">
         <button
            class="navbar-toggler"
            type="button"
            data-toggle="collapse"
            data-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent"
            aria-expanded="false"
            aria-label="Toggle navigation"
         >
            <span class="navbar-toggler-icon"></span>
         </button>

         <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
               <li class="nav-item active">
                  <router-link to="/home" class="nav-link">
                     <i class="fa-solid fa-house"></i>
                     Home
                  </router-link>
               </li>
               <li class="nav-item">
                  <router-link to="/contact" class="nav-link">
                  <i class="fa-solid fa-phone icon-phone"></i>
                  Liên hệ
                  </router-link>
               </li>
               <li class="nav-item">
                  <router-link to="/cart" class="nav-link">
                     Giỏ hàng
                     <i class="fa-solid fa-cart-shopping"></i>
                  </router-link>
               </li>
               <li class="nav-item count_products-cart">
                  <router-link to="/cart">
                     {{ localCarts.length }}
                  </router-link>
               </li>
               <li class="nav-item user_name" v-if="this.localUser.role != ''">
                  <router-link to="/" class="nav-link" @click="handleLogout">
                     <b>{{ this.localUser.name }}</b>
                     <button class="btn btn-primary logout-btn">
                        <i class="fa-solid fa-right-from-bracket"></i>
                     </button>
                  </router-link>
               </li>
               <li class="nav-item" v-if="this.localUser.role === 'admin'">
                  <router-link to="/admin" class="nav-link">
                     <button class="btn btn-primary admin-btn">
                        <i class="fa-solid fa-people-roof"></i>
                     </button>
                  </router-link>
               </li>
            </ul>
         </div>
      </nav>
   </div>
</template>

<script>
export default {
   data() {
      return {
         localUser: {},
         localCarts: {},
      };
   },
   methods: {
      handleLogout() {
         localStorage.removeItem("localUserLogin");
      },
   },
   mounted() {
      const user = JSON.parse(localStorage.getItem("localUserLogin"));
      this.localUser = user;
      const localProductCart = JSON.parse(
         localStorage.getItem("localProductCart") ?? "[]"
      );
      this.localCarts = localProductCart;
   },
};
</script>

<style>
@font-face {
   font-family: 'nunito';
   src: url(./src/fonts/Nunito/Nunito-Italic-VariableFont_wght.ttf) format('truetype');
   font-style: normal;
   font-weight: normal;
 }

.container {
   margin: 0 auto;
}
.container-fluid {
   padding: 0 0;
}
.navbar {
   border-top: 1px solid #d6d6d6;
   border-bottom: 3px solid #d6d6d6;
   border-right: 0;
   border-left: 0;
}
.navbar .nav-item {
   color: #fff;
   position: relative;
}
.navbar .nav-item a {
   font-family: 'Nunito';
   color: #555 !important;
   text-align: left;
   font-size: 20px;
   margin-left: 15px;
}
.navbar .nav-item a:hover {
   color: #040709 !important;
   background-color: #d6d6d6;
   list-style: none !important;
}
.nav-item ul li a {
   display: flex;
   text-align: left;
}
.dropdown-menu {
   width: 1031px;
   display: none;
   position: absolute;
   background: #fff;
   z-index: 1;
   border-top: 3px solid #3e7cb4;
   border-bottom: 0 none;
   border-left: 0 none;
   border-right: 0 none;
   font-size: 16px;
   padding: 10px 0;
   margin-top: 0;
   margin-left: -34px;
   border-radius: 0%;
}
.dropdown-menu ul {
   position: relative;
   z-index: 500;
   left: -15px;
   right: 0;
   list-style: none;
   padding-left: 0px;
   margin-left: 0;
}
.nav-item:hover .dropdown-menu {
   display: block;
}
.user_name {
   margin-left: 400px;
   text-transform: uppercase;
}
.logout-btn {
   width: 30px;
   height: auto;
   padding: 0px !important;
   margin-top: -5px;
   margin-left: 5px;
}
.admin-btn {
   width: 30px;
   height: auto;
   padding: 0px !important;
   margin-top: -5px;
}
.count_products-cart {
   left: -8px;
   top: 2px;
}
@media (min-width: 992px){
.navbar-expand-lg .navbar-nav .nav-link {
   padding-right: 0 !important;
    padding-left: 0.5rem !important;
   }
}

.btn-primary {
   color: #fff;
   background-color: #020a0c !important;
   border-color: #007bff;
}

</style>
