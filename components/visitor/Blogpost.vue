<script setup>
import { ArrowNarrowRightIcon } from "@heroicons/vue/solid";
import readmore from "@/assets/svg/readmore.svg?url";

const blogs = [
  {
    id: 1,
    img: "/images/blog_post_1.jpg",
    catg: "TECHNOLOGY",
    date: "19 Jan 2022",
    title: "Hey! Today let's introduce you to AWAQI",
    link: "blogs-id-blogDetail",
  },
  {
    id: 2,
    img: "/images/blog_post_2.jpg",
    catg: "TECHNOLOGY",
    date: "19 Jan 2022",
    title:
      "HaHuJobs have signed an MoU with the Ethiopian Investment Commission",
    link: "blogs-id-blogDetail",
  },
  {
    id: 3,
    img: "/images/blog_post_3.jpg",
    catg: "TECHNOLOGY",
    date: "19 Jan 2022",
    title: "ALx Software Engineering training",
    link: "blogs-id-blogDetail",
  },
];

const target = ref(null);
const observer = shallowRef();
const delay = [0, 150, 300];

onMounted(() => {
  observer.value = new IntersectionObserver((entries) => {
    entries.forEach(
      (entry) => {
        entry.target.classList.toggle(
          "lg:[&[show=true]]:opacity-100",
          entry.isIntersecting
        );
        entry.target.classList.toggle(
          "lg:[&[show=true]]:translate-y-0",
          entry.isIntersecting
        );
        entry.target.classList.toggle(
          "lg:[&[show=true]]:translate-x-0",
          entry.isIntersecting
        );
        if (entry.isIntersecting) {
          observer.value.unobserve(entry.target);
          return entry.target;
        }
      },
      {
        threshold: 0.5,
      }
    );
  });
  target.value.forEach((card) => {
    observer.value.observe(card);
  });
});

onBeforeUnmount(() => {
  observer.value.disconnect();
});
</script>

<template>
  <section v-for="i in 1" class="mt-10 flex flex-col" id="blog">
    <div class="flex flex-col items-center">
      <h1 show="true" ref="target"
        class="mt-10 lg:opacity-0 lg:translate-y-20 lg:duration-1000 self-center text-lg font-medium leading-[18px] dark:text-white lg:mt-[90px]">
        Blog
      </h1>
      <div show="true" ref="target" class="flex lg:opacity-0 lg:translate-y-20 lg:duration-1000 mt-9">
        <NuxtLink :to="{ name: 'blogs' }" class="self-center">
          <button
            class="gap-2 group flex items-center rounded-[36px] bg-primary-lite px-3 py-2 text-center text-base font-black leading-5 text-white duration-300 hover:translate-x-1 hover:-translate-y-1 hover:shadow-2xl active:translate-x-0 active:translate-y-0 active:shadow-none xs:px-8 xs:text-lg lg:px-5 3xl:px-8 3xl:py-4 lg:py-2 lg:text-2xl 3xl:text-3xl lg:leading-[18px]">
            Recent Blogs
            <img :src="readmore" class="text-white h-4 3xl:h-6 xl:scale-0 group-hover:scale-100 duration-300"
              alt="button" />
          </button>
        </NuxtLink>
      </div>
      <p show="true" ref="target"
        class="mt-[34px] lg:opacity-0 lg:translate-y-20 lg:duration-1000 max-w-[900px] text-center text-base font-light leading-[30px] dark:text-HahuGray/4 xs:text-lg">
        Below are some of our updates regarding our ventures with in the labor
        market and our partners offers in regards to related endeavors
      </p>
    </div>

    <div class="mt-16 grid grid-cols-1 justify-items-center gap-x-5 gap-y-10 lg:grid-cols-3">
      <div show="true" ref="target"
        class="flex max-w-[560px] lg:opacity-0 lg:-translate-x-40 lg:duration-700 flex-col rounded-b-[15px] bg-white dark:bg-HahuGray1 hover:scale-[1.01] active:scale-100 border-2 border-transparent hover:border-primary hover:shadow-xl"
        :class="`delay-${delay[i]}`" v-for="(blog, i) in blogs" :key="i">
        <NuxtLink :to="'/blogs/' + blog.id" class="flex flex-col">
          <div>
            <img class="object-cover" :src="blog.img" alt="blogImage" />
          </div>
          <h1
            class="mt-6 ml-8 self-start rounded-[36px] bg-primary-lite px-3 py-[5px] text-xs font-medium leading-[18px] text-primary-dark">
            {{ blog.catg }}
          </h1>
          <h4 class="mt-4 ml-8 text-base font-medium leading-6">
            {{ blog.date }}
          </h4>
          <p class="mt-4 ml-8 pr-[24px] text-xl font-bold leading-[38px] dark:text-HahuGray/4 3xl:text-2xl">
            {{ blog.title }}
          </p>
          <button class="group mt-[34px] ml-8 mb-[30px] flex items-center self-start text-lg font-medium text-primary">
            Read Post
            <ArrowNarrowRightIcon class="ml-[9px] w-[18px] text-primary duration-200 group-hover:translate-x-1" />
          </button>
        </NuxtLink>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
</style>
