<script setup>
import { RouterLink, RouterView } from 'vue-router'
import { ref, watch ,computed  } from "vue";
import Dashboard from './Dashboard.vue'

const emits = defineEmits(['menu'])


// layout menu start
const items = ref([
    {
        id: 1,
        name: 'Dashboard',
        link: '/dashboard',
        type: false,
        click_type: false,
        item: [
            {
                id: 1,
                name: 'home',
                type: false,
                click_type: false,
            },
            {
                id: 2,
                name: 'Diagramma',
                type: false,
                click_type: false,
            },
            {
                id: 3,
                name: 'Statistica',
                type: false,
                click_type: false,
            }
        ]
    },
    {
        id: 2,
        name: 'About',
        link: '/about',
        type: false,
        click_type: false,
        item: [
            {
                id: 4,
                name: 'about me',
                type: false,
                click_type: false,
            },
            {
                id: 5,
                name: 'about me',
                type: false,
                click_type: false,
            },
            {
                id: 6,
                name: 'about me',
                type: false,
                click_type: false,
            },
            {
                id: 7,
                name: 'about me',
                type: false,
                click_type: false,
            }
        ]
    }
])

// Parent btn start 
const parent_send = (item) => {

    console.log(item)
    item.click_type = !item.click_type;
    for (let index = 0; index < item.item.length; index++) {
        const element = item.item[index];

        element.click_type = !element.click_type;
        console.log(element)
    }
}
// Parent btn end 

// __________Child btn start
const child_btn = (item, i) => {
    console.log(item, i);
    let count = 0;
    i.click_type = !i.click_type;
    for (let index = 0; index < item.item.length; index++) {
        const element = item.item[index];
        if (element.click_type === true) {
            count += 1
        }
        if (element.click_type === false) {
            count -= 1
        }
    }
    if (item.item.length === count) {
        item.click_type = true
    }
    else if (item.item.length > count) {
        item.click_type = false
    }
}
// ___________Child btn end


// menu data opionst start
const parentData = ref([
    {
        id: 1,
        name: 'Dashboard'
    },
    {
        id: 2,
        name: 'Navbar'
    },
    {
        id: 3,
        name: 'Logo'
    },
    {
        id: 4,
        name: 'Footer'
    },
    {
        id: 5,
        name: 'Testlash uchun'
    },
    {
        id: 6,
        name: 'Navbar test'
    },
    {
        id: 7,
        name: 'test uchun'
    },
    {
        id: 8,
        name: 'Test'
    }
]);
const child = ref([]);

// menu send props start
// const send = (item) => {
//     console.log(item)
//     child.value = item
// }
const send = (event) => {
    child.value = JSON.parse(event.target.value);
};

let  filteredItems = computed(() => {
  return items.value.filter(item => item.name.toLowerCase().includes(searchTerm.value.toLowerCase()));
});

const searchTerm = ref('');
</script>
<template>
    <div class="mains">

        <div class="layout">

            <div class="container">
                <select @change="send" class="select">
                    <option v-for="(item, index) in parentData" :key="index" :value="JSON.stringify(item)">{{ item.name
                        }}
                    </option>
                </select>

                <input class="select" type="text" v-model="searchTerm" placeholder="Mant kiritish..." >
                
                <div v-if="filteredItems.length > 0" v-for="item in filteredItems" :key="item.id" type="none" style="min-width:250px;">

                    <div class="title">

                        <div @click="parent_send(item)">

                            <div class="click_type" v-if="item.click_type === false">

                            </div>
                            <div class="click" v-if="item.click_type === true">
                                <svg style="color: #fff; margin-top: -2px; margin-left: -2px;"
                                    xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24">
                                    <path fill="none" stroke="currentColor" stroke-linecap="round"
                                        stroke-linejoin="round" stroke-width="2" d="M5 11.917L9.724 16.5L19 7.5" />
                                </svg>
                            </div>

                        </div>

                        <div>{{ item.name }}</div>
                        <svg @click="item.type = !item.type" xmlns="http://www.w3.org/2000/svg" width="20" height="26"
                            viewBox="0 0 24 24">
                            <path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                                stroke-width="2" d="m19 9l-7 7l-7-7" />
                        </svg>

                    </div>
                    <div v-for="i in item.item" :key="i.id" type="none" v-if="item.type === true">

                        <div style="display: flex; gap: 10px; margin-left: 40px;">
                            <div @click="child_btn(item, i)">

                                <div class="click_type" v-if="i.click_type === false">

                                </div>
                                <div class="click" v-if="i.click_type === true">
                                    <svg style="color: #fff; margin-top: -2px; margin-left: -2px;"
                                        xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24">
                                        <path fill="none" stroke="currentColor" stroke-linecap="round"
                                            stroke-linejoin="round" stroke-width="2" d="M5 11.917L9.724 16.5L19 7.5" />
                                    </svg>
                                </div>

                            </div>
                            <RouterLink :to="i.link">{{ i.name }}</RouterLink>
                        </div>

                    </div>

                </div>

            </div>

        </div>

        <Dashboard :info="child" class="dashboard" />
        <!-- <RouterView /> -->

    </div>

</template>
<style>
.dashboard {
    width: 100%;
}

.mains {
    display: flex;
    justify-content: space-around;
    height: 100vh;
    width: 100%;
}

.layout {
    height: 100vh;
    width: 250px;
    background-color: #fff;
}

.title {
    display: flex;
    width: 250px;
    gap: 20px;
    margin: 10px;
    cursor: pointer;
}

.container {
    width: 90%;
    margin: 20px auto;
}

.click_type {
    height: 20px;
    width: 20px;
    border: 1px solid #ccc;
    border-radius: 4px;
    margin-top: 4px;
}

.click {
    height: 20px;
    width: 20px;
    border: 1px solid #ccc;
    border-radius: 4px;
    margin-top: 4px;
    background-color: rgb(236, 13, 13);
}

.select {
    width: 200px;
    margin: 0 auto;
    height: 30px;
    margin-top: 10px;
    position: relative;
}
.select-search {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0;
}
</style>