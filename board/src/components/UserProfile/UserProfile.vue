<script setup>
import { onMounted } from 'vue';
import { useUserStore } from '@/stores/user'
import { storeToRefs } from 'pinia';

const userStore = useUserStore()
const { user, tmpUser } = storeToRefs(userStore)

onMounted(() => {
  tmpUser.value = JSON.parse(JSON.stringify(user.value));
})
</script>
<template>
    <div class="container">
        <div class="col-5 align-items-center">
            <div class="mb-1 bg-white">
                <div class="w-auto d-flex justify-content-center align-items-center flex-column mx-2">
                    <div class="m-2">個人資料</div>
                </div>
                <div class="w-auto d-flex align-items-center flex-column border-top">
                    <img src="../../assets/logo.svg" alt="" class="my-4">
                    <div class="m-2">{{ user.account }}</div>
                    <div v-if="user.intro != ''">
                        {{ user.intro }}
                    </div>
                    <div v-else>可以新增個人簡介</div>
                </div>
            </div>
        </div>
        <div class="mb-1 bg-white">
            <div class="w-auto d-flex align-items-center flex-column mx-2">
                <div class="m-2">資料修改</div>
            </div>
            <!-- 編輯個人資料 -->
            <div class="w-auto d-flex align-items-center flex-column border-top mx-2">
                <img class="head-img my-4" src="../../assets/logo.svg" />
                <div class="m-2">使用者名稱</div>
                <form @submit.prevent="userStore.editUser()" class="w-100 px-3">
                    <div class="d-flex justify-content-center align-items-center py-2">
                        <label for="inputAccount" class="d-flex col-3">帳號名</label>
                        <input type="text" class="form-control" id="inputAccount" v-model="tmpUser.account">
                    </div>
                    <div class="d-flex justify-content-center align-items-center py-2">
                        <label for="inputEmail" class="d-flex col-3">信箱</label>
                        <input type="email" class="form-control" id="inputEmail" v-model="tmpUser.email">
                    </div>
                    <div class="d-flex justify-content-center align-items-center py-2">
                        <label for="inputIntro" class="d-flex col-3">個人簡介</label>
                        <textarea type="text" class="form-control" id="inputIntro" v-model="tmpUser.intro"></textarea>
                    </div>
                    <div class="d-flex justify-content-center align-items-center py-2">
                        <label for="inputPassword" class="d-flex col-3">密碼</label>
                        <input type="text" class="form-control" id="inputPassword" v-model="tmpUser.password">
                    </div>
                    <div class="d-flex justify-content-center align-items-center py-2">
                        <label for="inputPasswordCheck" class="d-flex col-3">再次密碼</label>
                        <input type="text" class="form-control" id="inputPasswordCheck" v-model="tmpUser.pass_check">
                    </div>
                    <div class="d-flex justify-content-evenly align-items-center">
                        <a href="./UserProfile.vue" class="text-primary text-decoration-none">取消</a>
                        <button type="submit" class="btn bnt-primary px-5">儲存</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>