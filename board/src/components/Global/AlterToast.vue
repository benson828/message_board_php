<script setup>
import { useToastStore } from '@/stores/alterToast'
import { storeToRefs } from 'pinia'
const toastStore = useToastStore()
  const { toastData } = storeToRefs(toastStore)
</script>
<template>
  <div class="d-flex position-fixed ">
    <div id="liveToast" class="toast" role="alert" aria-live="assertive" aria-atomic="true">
      <!-- 修改失敗 -->
      <div class="toast-header text-center bg-danger" v-if="toastData.status == 'error'">
        <strong class="me-auto">{{ toastData.event }}</strong>
        <button type="button" class="btn-close" data-bs-dismiss="toast" aria-label="close"></button>
      </div>
      <!-- 修改成功 -->
      <div class="toast-header text-center bg-success" v-if="toastData.status == 'success' || toastData.status == 'cancel'">
        <strong class="me-auto">{{ toastData.event }}</strong>
        <button type="button" class="btn-close" data-bs-dismiss="toast" aria-label="close"></button>
      </div>
      <div class="toast-body">{{ toastData.content }}</div>
    </div>
  </div>
</template>