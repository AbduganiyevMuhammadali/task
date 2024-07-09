<script setup>

import { ref, watch } from "vue";

const props = defineProps(['info'])

const items = ref([])


watch(() => props.info, val => {
    items.value.push(val)
})

const deleteItem = (itemToDelete) => {
  items.value = items.value.filter((item) => item.id !== itemToDelete.id);
};
</script>
<template>
    <div class="cards">
        <div v-for="item in items" :key="item.id" >
            <div class="card">
                <span>{{item.name}}</span>
                <div class="card-btn">
                    <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24"><path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6m0 12L6 6"/></svg>
                    <div class="card-btn-delete" @click="deleteItem(item)">
                       <div class="card-btn-delete-text">
                           Delete
                        <svg style="margin-top: 4px;" xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24"><path fill="currentColor" fill-rule="evenodd" d="M8.586 2.586A2 2 0 0 1 10 2h4a2 2 0 0 1 2 2v2h3a1 1 0 1 1 0 2v12a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V8a1 1 0 0 1 0-2h3V4a2 2 0 0 1 .586-1.414M10 6h4V4h-4zm1 4a1 1 0 1 0-2 0v8a1 1 0 1 0 2 0zm4 0a1 1 0 1 0-2 0v8a1 1 0 1 0 2 0z" clip-rule="evenodd"/></svg>
                       </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped>
.cards{
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    margin-left: 30px;
    width: 1000px;
    margin-top: 30px;
}
.card {
    text-align: center;
    position: relative;
    display: flex;
   padding: 5px 14px;
   gap: 10px;
   border-radius: 6px;
   box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.1);
   background-color: #fff;
   font-weight: bold;
   font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}
.card-btn{
    margin-top: 3px;
    cursor: pointer;
    position: relative;
}
.card:hover .card-btn-delete{
   display: block;
}
.card-btn-delete{
   animation: alternate 0.5s;
    
    display: none;
    position: absolute;
    border-radius: 1px solid red;
    border-radius: 4px;
    background-color: red;
    color: white;
    padding: 2px 4px;
    font-weight: bold;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    cursor: pointer;
    top: 30px;
    left: -10px;
}
.card-btn-delete-text{
    display: flex;
}
</style>