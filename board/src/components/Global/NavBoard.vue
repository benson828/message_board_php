<script setup>
import { onMounted } from 'vue'
import { useUserStore } from '@/stores/user'
import { storeToRefs } from 'pinia'

const userStore = useUserStore()
const { user } = storeToRefs(userStore)

onMounted(() => {
  console.log('mounted!')
})
</script>
<template>
<!-- 導覽列 -->
  <nav class="navbar navbar-expand-lg">
    <router-link class="navbar-brand" :to="'/'">CMRDB-Board</router-link>
    <div class="d-flex justify-content-between align-items-center " v-if="user.user_id ==''">
      <button 
      class="btn btn-light mx-auto"
      data-bs-toggle="modal"
      data-bs-target="#loginModalUI"
      aria-hidden="true"
      >
      登入 / 註冊
      </button>
    </div>
    <div class="" v-else>
      <img class="user_img" src="../../assets/logo.svg" >
      <ul class="navbar-nav">
        <li class="nav-item dropdown">
          <a 
          href="#" 
          class="nav-link dropdown-toggle" 
          role="button" 
          data-bs-toggle="dropdown" 
          aria-expanded="false">
          {{ user.account }}
          </a>
          <ul>
            <li>
              <router-link class="dropdown-item" :to="'/userProfile'" replace>個人資料</router-link>
            </li>
                <li><hr class="dropdown-divider"></li>
            <li>
              <router-link class="dropdown-item" :to="'/'" @click="userStore.signOut()" replace>登出</router-link>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </nav>
  <!-- 登入介面 -->
  <div class="modal fade" id="loginModalUI" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered" role="document">
      <div class="modal-content">
        <form @submit.prevent="userStore.login()">
          <div class="modal-header">
            <h5 class="modal-title">登入</h5>
          </div>
          <div class="d-flex justify-content-center">
            <label for="userName" class="d-flex justify-content-center">帳號</label>
            <input type="text" name="userName" id="userName" v-modal="user.account">
          </div>
          <div class="">
            <label for="userPassword" id="inputPassword">密碼</label>
            <input type="password" class="form-control" id="inputPassword" v-model="user.password">
          </div>
          <div class="d-flex justify-content-evenly align-items-center">
            <a class="text-primary" data-bs-toggle="modal" data-bs-target="#registerModalUI">尚未有帳戶</a>
            <button type="submit" class="btn btn-primary" data-bs-dismiss="modal">登入</button>
          </div>
        </form>
      </div>
    </div>
  </div>
<!-- 註冊介面 -->
<div class="modal fade" id="registerModalUI" tabindex="-1">
  <div class="modal-dialog modal-dialog-centered ">
    <div class="modal-content container">
      <form @submit.prevent="userStore.register()">
        <div class="modal-header justify-content-center">
          <h5 class="title">註冊</h5>
        </div>
        <div class="d-flex justify-content-center align-items-center">
          <label class="d-flex justify-content-center col-3" for="userName">帳號</label>
          <input type="text" class="form-control col-6" id="userName" v-modal="user.account">
        </div>
        <div class="d-flex justify-content-center align-items-center">
            <label class="d-flex justify-content-center col-3" for="userEmail">信箱</label>
            <input type="text" class="form-control col-6" id="userEmail" v-modal="user.email">
          </div>
        <div class="d-flex justify-content-center align-items-center">
          <label class="d-flex justify-content-center col-3" for="inputPassword">密碼</label>
          <input type="password" class="form-control col-6" id="inputPassword" v-modal="user.password">
        </div>
         <div class="d-flex justify-content-center align-items-center">
            <label for="inputPassword" class="d-flex justify-content-center col-3">再次輸入密碼</label>
              <input type="password" class="form-control col-6" id="inputPassword" v-model="user.pass_check">
          </div>
          <div class="d-flex justify-content-evenly align-items-center">
            <a data-bs-toggle="modal" data-bs-target="#loginModalUI" class="text-primary">已有帳號</a>
          </div>
          <div>
            <button type="submit" class="btn btn-success" data-bs-dismiss="modal">註冊</button>
          </div>
      </form>
    </div>
  </div>
</div>
</template>
<style>
.header-nav {
  background-color: #242f42;
  color: aliceblue;
  padding: 0.5rem;
}

.head-img {
  border-radius: 100%;
  width: 3rem;
}
</style>