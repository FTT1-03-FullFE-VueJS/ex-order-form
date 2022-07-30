<template>
    <div class="main">
        <h1>Services</h1>
        <ul>
            <li
                v-for="service in services"
                :key="service.id"
                :class="{
                    active: servicesIdsActive.includes(service.id)
                }"
                @click="serviceClickHandler(service.id)"
            >
                <span class="name">{{ service.name }}</span>
                <span class="price">${{ service.price }}</span>
            </li>
        </ul>
        <div class="total">
            <span>Total:</span>
            <span>${{totalPrice}}</span>
        </div>
    </div>
</template>

<script setup>
import { ref, watch, computed } from 'vue';
/**
 * ServicesIdsActive dùng để lưu những id được click vàovào
 */
const servicesIdsActive = ref([]);

/**
 * Service dùng để lưu danh sáchh những service được hiển thị trên mànn hình.
 */
const services = ref([
    {
        id: 1,
        name: 'Web Development',
        price: 300
    },
    {
        id: 2,
        name: 'Design',
        price: 400
    },
    {
        id: 3,
        name: 'Integration',
        price: 500
    },
    {
        id: 4,
        name: 'Training',
        price: 600
    },
]);

const totalPrice = computed(() => {
    let total = 0;
    services.value.forEach(service => {
        if (servicesIdsActive.value.includes(service.id)) {
            total += service.price;
        }
    });

    return total;
});

// watch(servicesIdsActive, (curr, prev) => {
//     console.log(curr);
// })

const serviceClickHandler = (id) => {// 1
    if (servicesIdsActive.value.includes(id)) {
        // [1, 2, 3, 4]
        const newServiceIds = servicesIdsActive.value.filter(serviceId => serviceId !== id);
        servicesIdsActive.value = newServiceIds;
    } else {
        const newServiceIds = [...servicesIdsActive.value, id];
        servicesIdsActive.value = newServiceIds;
    }
}
</script>

<style>
.main {
    width: 500px;
    border: 1px solid #ccc;
    padding: 10px;
    background: #61a1bc;
}
h1 {
    color: #fff;
    font-size: 64px;
    font-family: 'Cookie', cursive;
    font-weight: normal;
    line-height: 1;
    text-shadow: 0 3px 0 rgb(0 0 0 / 10%);
    text-align: center;
    margin-bottom: 30px;
}
ul {
    list-style-type: none;
    padding: 0;
}
li {
    padding: 15px 30px;
    background-color: #e35885;
    margin-bottom: 8px;
    box-shadow: 0 1px 1px rgb(0 0 0 / 10%);
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: #fff;
    font-weight: bold;
    font-size: 20px;
}
.total {
    border-top: 1px solid rgba(255,255,255,0.5);
    padding: 15px 30px;
    font-size: 20px;
    font-weight: bold;
    text-align: left;
    color: #fff;
    display: flex;
    justify-content: space-between;
    align-items: center;
}
ul li.active {
    background-color: #8ec16d;
}
</style>
