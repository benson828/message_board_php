<script setup>
import { useCommentStore } from '@/stores/comment'
import { storeToRefs } from 'pinia'
const commentStore = useCommentStore()
const { newAdd } = storeToRefs(commentStore)
</script>
<template>
    <div class="position-bottom p-3">
        <button class="btn bnt-light" data-bs-toggle="modal" data-bs-target="#addCommentModalUI" aria-hidden="true">
                  <img class="head-img my-4" src="../../assets/add.png" />
        </button>
        <div class="modal fade" id="addCommentModalUI" tabindex="-1" aria-labelledby="addCommentModal">
            <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
                <div class="modal-content">
                    <form @submit.prevent="commentStore.createComment()">
                        <div class="modal-header justify-content-center align-items-center">
                        <h5>新增留言</h5>
                        </div>
                        <div class="d-flex justify-content-center align-items-center">
                            <label for="inputTittle" class="d-flex col-3 justify-content-center">標題</label>
                            <input type="text" class="form-control col-6" id="inputTittle" v-model="newAdd.tittle">
                        </div>
                        <div class="d-flex justify-content-center align-items-center">
                                <label for="inputContent" class="d-flex col-3 justify-content-center">內文</label>
                                <input type="text" class="form-control col-6" id="inputContent" v-model="newAdd.content">
                        </div>
                        <div>
                            <button type="submit" class="btn btn-primary px-5" data-bs-dismiss="modal0">新增</button>
                            <button type="submit" class="btn btn-outline-secondary px-5" data-bs-dismiss="modal0">刪除</button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>