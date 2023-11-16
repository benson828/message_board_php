<script setup>
import { useCommentStore } from '@/stores/comment'
import { storeToRefs } from 'pinia'

const commentStore = useCommentStore()
const { search } = storeToRefs(commentStore)
</script>
<template>
    <div class="container p-3">
        <form @submit.prevent="commentStore.searchComment()" class="d-flex w-100">
            <div class="d-flex flex-column col-9 px-5">
                <div class="d-flex my-2">
                    <div class="col-2 d-flex align-items-center">查詢時間範圍：</div>
                    <div class="col-10 d-flex justify-content-between">
                        <input type="datetime-local" class="btn rounded-0" v-model="search.first_time">
                        <div class="d-flex align-items-center">~</div>
                        <input type="datetime-local" class="btn rounded-0" v-model="search.last_time">
                    </div>
                </div>
                <div class="my-2">
                    <input type="text" class="form-control" placeholder="搜尋關鍵字" v-model="search.search_content">
                </div>
            </div>
            <div class="d-flex flex-column col-2 ">
                <button type="submit" class="btn btn-primary">搜尋</button>
                <button type="button" class="btn btn-light" @click="commentStore.clearSearch()">重製</button>
            </div>
        </form>
    </div>
</template>
