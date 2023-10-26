<!-- some-inner-component.vue -->
<template>
  <p>
    page {{ pageNum }} is {{ swiperSlide.isActive ? "active" : "not active" }}
  </p>
</template>
<script setup>
import { useSwiperSlide } from "swiper/vue";
import { ref, watch } from "vue";

const props = defineProps({
  pageNum: Number,
});

const swiperSlide = useSwiperSlide();

let change = ref(true);

let pageMessage = ref([
  {
    pageNumber: 1,
    pageIsActive: false,
  },
  {
    pageNumber: 2,
    pageIsActive: false,
  },
  {
    pageNumber: 3,
    pageIsActive: false,
  },
  {
    pageNumber: 4,
    pageIsActive: false,
  },
]);

watch(swiperSlide, () => {
  if (swiperSlide.value.isActive) {
    // console.log(props.pageNum);
    pageMessage.value[props.pageNum - 1] = {
      pageNumber: props.pageNum,
      pageIsActive: swiperSlide.value.isActive,
    };
    // console.log("child emit")
    const messageString = JSON.stringify(pageMessage.value);
    localStorage.setItem("message", messageString);
  }
});
</script>
