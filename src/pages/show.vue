<template>
    <swiper
            :scrollbar="{hide: false}"
            :modules="modules"
            class="mySwiper"
            @swiper="onSwiper"
            @slideChange="onSlideChange"
    >
        <swiper-slide><PageMessage :pageNum=1></PageMessage></swiper-slide>
        <swiper-slide><PageMessage :pageNum=2></PageMessage></swiper-slide>
        <swiper-slide><PageMessage :pageNum=3></PageMessage></swiper-slide>
        <swiper-slide><PageMessage :pageNum=4></PageMessage></swiper-slide>
    </swiper>
    <div class="bottomNav">
        <div class="bottomNavItem partOne" :class="{ active: ActivePageNum === 1 }" @click="isActiveItem(1)">part 1</div>
        <div class="bottomNavItem partTwo" :class="{ active: ActivePageNum === 2 }" @click="isActiveItem(2)">part 2</div>
        <div class="bottomNavItem partThree" :class="{ active: ActivePageNum === 3 }" @click="isActiveItem(3)">part 3</div>
        <div class="bottomNavItem partFour" :class="{ active: ActivePageNum === 4 }" @click="isActiveItem(4)">part 4</div>
    </div>
</template>
<script setup>
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Scrollbar } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/scrollbar';
import './show.css'
import PageMessage from "../components/pageMessage.vue";
import { ref } from "vue";


let ActivePageNum = ref(1);
let pageMessage = ref();
let ActivePage = ref();
let swiperRef = ref();

const onSwiper = (swiper) => {
    swiperRef.value = swiper;
};

const onSlideChange = () => {
    let messageString ;
    setTimeout(()=>
    {
        messageString = localStorage.getItem('message');
        pageMessage.value = JSON.parse(messageString);
        ActivePage.value = pageMessage.value.find(item => item.pageIsActive === true);
        ActivePageNum.value = ActivePage.value.pageNumber;
    },0)
};

const modules =  [Scrollbar]

function isActiveItem(index){
    swiperRef.value.slideTo(index-1);
}

</script>