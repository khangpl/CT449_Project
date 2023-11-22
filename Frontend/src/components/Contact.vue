<template>
   <div class="wrapper">
      <div class="header">
         <div class="nav-menu">
            <NavMenu />
         </div>
      </div>
      <div class="container">
         <p>
            <i class="fa-solid fa-location-dot"></i>
            <a href="https://ctu.edu.vn">
               Trường Đại Học Cần Thơ Khu II, Đ. 3/2, Xuân Khánh, Ninh Kiều, Cần
               Thơ
            </a>
         </p>
         <p>
            <i class="fa-solid fa-school"></i>
            Khoa công nghệ thông tin và truyền thông
         </p>
         <p>
            <i class="fa-solid fa-envelope icon-email"></i>
            tranvinhkhang123t@gmail.com
         </p>
         <p>
            <i class="fa-solid fa-phone icon-phone"></i>
            +84 832723464
         </p>

         <div class="form-group row">
            <label class="col-sm-2 col-form-label">Phản hồi, Góp ý</label>
            <div class="col-sm-8">
               <textarea class="form-control" row="7"> </textarea>
               <button
                  type="submit"
                  class="btn btn-primary mt-2 float-left"
                  @click="feedback"
               >
                  Gửi
               </button>
               <button type="reset" class="btn btn-danger mt-2 ml-2 float-left">
                  Xóa
               </button>
            </div>
         </div>
      </div>
   </div>
</template>

<script>
import NavMenu from "../components/NavMenu.vue";

export default {
   components: {
      NavMenu,
   },
   methods: {
      feedback() {
         alert("Cảm ơn bạn đã đóng góp ý kiến!!");
      },
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

 p{
   font-family: 'Nunito';
 }

 .form-group{
   font-family: 'Nunito';
 }
.wrapper {
   max-width: 100%;
   background-color: #fff;
   font-family: "Open Sans", sans-serif;
   padding-bottom: 50px;
}
.header {
   width: 100%;
   height: auto;
}
.container {
   text-align: center;
   margin-top: 10px;
   color: #333;
}
</style>
