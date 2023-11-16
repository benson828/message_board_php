<script setup>
import { useUserStore } from '@/stores/user'
import { storeToRefs } from 'pinia';
const userStore = useUserStore()
const { user } = storeToRefs(userStore)
</script>
<template>
    <div class="container">
        <div class="col-7">
            <div class="mb-1 bg-white">
                <div class="m-2 w-auto d-flex align-items-center text-center">自己所有留言</div>
                <div class="w-auto d-flex align-items-center border-top">
                    <img src="../../assets/logo.svg" alt="" class="head-img my-4">
                    <div class="m-2">{{ user.account }}</div>
                    <div class="m-2">個人簡介</div>
                </div>
            </div>
        </div>

    </div>
</template>