<template>
  
   <div class="container">
      <div class="d-flex justify-content-center h-100">
         <div class="card">
            <div class="card-header text-center">
               <h3>Đăng nhập</h3>
            </div>
            <div class="card-body">
               <form @submit.prevent="login()">
                  <div class="input-group form-group">
                     <div class="input-group-prepend">
                        <span class="input-group-text">
                           <i class="fa-solid fa-envelope"></i>
                        </span>
                     </div>
                     <input
                        type="email"
                        class="form-control"
                        placeholder="Email"
                        @blur="validate()"
                        v-model="user.email"
                        :class="{ 'is-invalid': errors.email }"
                     />
                     <div class="invalid-feedback" v-if="errors.email">
                        {{ errors.email }}
                     </div>
                  </div>
                  <div class="input-group form-group">
                     <div class="input-group-prepend">
                        <span class="input-group-text"
                           ><i class="fas fa-key"></i
                        ></span>
                     </div>
                     <input
                        type="password"
                        class="form-control"
                        placeholder="Mật khẩu"
                        @blur="validate()"
                        v-model="user.password"
                        :class="{ 'is-invalid': errors.password }"
                     />
                     <div class="invalid-feedback" v-if="errors.password">
                        {{ errors.password }}
                     </div>
                  </div>
                  <div class="form-group">
                     <input
                        type="submit"
                        value="Đăng nhập"
                        class="btn login_btn"
                     />
                  </div>
               </form>
            </div>
            <div class="card-footer">
               <div class="d-flex justify-content-center links">
                  <p>
                     Nếu bạn chưa có tài khoản!
                     <router-link to="/register">ĐĂNG KÝ</router-link>
                  </p>
               </div>
            </div>
         </div>
      </div>
   </div>
</template>

<script>
import UserService from "../services/user.service";

export default {
   data() {
      return {
         errors: {
            email: "",
            password: "",
         },
         user: {
            email: "",
            password: "",
         },
      };
   },
   methods: {
      validate() {
         let isValid = true;

         this.errors = {
            email: "",
            password: "",
         };

         if (!this.user.email) {
            this.errors.email = "Email là bắt buộc";
            isValid = false;
         }

         if (!this.user.password) {
            this.errors.password = "Mật khẩu là bắt buộc";
            isValid = false;
         }
         return isValid;
      },
      async login() {
         if (this.validate()) {
            const userLogin = await UserService.login(this.user);
            const localUserLogin = JSON.stringify(userLogin);
            localStorage.setItem("localUserLogin", localUserLogin);
            if (userLogin.role === "user") {
               this.$router.push({ name: "home" });
            } else if (userLogin.role === "admin") {
               this.$router.push({ name: "admin" });
            } else {
               alert("Xin lỗi! Bạn đã nhập sai email hoặc mật khẩu!");
            }
         }
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

.container {
   padding-top: 100px;
   padding-bottom: 180px;
   margin-top: 10px;
}
.card {
   height: 370px;
   margin-top: auto;
   margin-bottom: auto;
   width:475px;
   background-color: rgba(1, 0, 0, 0.5) !important;
   border-radius: 40px;
}
.social_icon span {
   font-size: 60px;
   margin-left: 10px;
   color: #ffc312;
}
.social_icon span:hover {
   color: white;
   cursor: pointer;
}
.card-header h3 {
   font-family: 'Nunito';
   font-style: normal;
   font-weight: bold;
   color: white;
}
.social_icon {
   position: absolute;
   right: 20px;
   top: -45px;
}
.input-group-prepend span {
   width: 50px;
   background-color: #12ffe3;
   color: black;
   border-radius: 40px;
}
input:focus {
   outline: 0 0 0 0 !important;
   box-shadow: 0 0 0 0 !important;
}
.login_btn {
   color: rgb(0, 0, 0);
   background-color:#12ffe3;
   border-radius: 40px;
   width: 100px;
}
.login_btn:hover {
   color: #020202;
   background-color: rgb(225, 219, 219);
}
.links {
   color: white;
}
.links a {
   margin-left: 4px;
}
p{
   font-weight: bold !important;
}



</style>
