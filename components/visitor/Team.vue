<script setup>
import CEO from "@/assets/svg/CEO.svg?url";
import Law from "@/assets/svg/law.svg?component";
import Finance from "@/assets/svg/finance.svg?component";
import Project from "@/assets/svg/ProjectManager.svg?component";
import Support from "@/assets/svg/support.svg?component";
import Backend from "@/assets/svg/Devloper.svg?component";
import Design from "@/assets/svg/design.svg?component";
import Chat from "@/assets/svg/chat.svg?component";
import Recruiter from "@/assets/svg/recruiter.svg?component";

const team = [
  {
    name: "Kaleab Mezgebu",
    img: "/images/About_avatar.png",
    icon: CEO,
    pos: "COO/CEO",
    prov: "Manages all operations and resources under HaHuJobs",
  },
  {
    name: "Michael Sahlu ",
    img: "/images/About_avatar.png",
    icon: CEO,
    pos: "CTO",
    prov: "Manages all technical resources under HaHuJobs",
  },
  {
    name: "Eskindir mamo",
    img: "/images/About_avatar.png",
    icon: CEO,
    pos: "CBO",
    prov: "Manages business outreach of all HaHuJobs services",
  },

  // {
  //   name: "Jhon Doe",
  //   img: "/images/Attorney.png",
  //   icon: Law,
  //   pos: "Attorney",
  //   prov: "The only way to do great work is to love what you do.",
  // },
  // {
  //   name: "Jhon Doe",
  //   img: "/images/Finance.png",
  //   icon: Finance,
  //   pos: "Finance Manager",
  //   prov: "The only way to do great work is to love what you do.",
  // },

  // {
  //   name: "Jhon Doe",
  //   img: "/images/Backend.png",
  //   icon: Backend,
  //   pos: "Backend Developer",
  //   prov: "The only way to do great work is to love what you do.",
  // },
  // {
  //   name: "Jhon Doe",
  //   img: "/images/Graphics.png",
  //   icon: Design,
  //   pos: "Graphics Designer",
  //   prov: "The only way to do great work is to love what you do.",
  // },
];

const team2 = [{
  name: "Natnale Yared",
  img: "/images/About_avatar.png",
  icon: Chat,
  pos: "Communication manger",
  prov: "Natnael manages stakeholder or partner communication and market reach of the HaHuJobs brand",
},
{
  name: "Kalkidan Tesfamaria",
  img: "/images/About_avatar.png",
  icon: Project,
  pos: "Project Manager",
  prov: "Kalkidan overseas HaHuJobs Industrial Park services and day-to-day operations of regional offices",
},
{
  name: "Michale Shimelis",
  img: "/images/About_avatar.png",
  icon: Recruiter,
  pos: "Recruitment manager",
  prov: "Michale manages and coordinates digital job matching services of HaHuJobs via its employment centers",
},
{
  name: "Zelalem Mekonnen",
  img: "/images/About_avatar.png",
  icon: Backend,
  pos: "Development  Manager",
  prov: "Zelalem directs and coordinates all HaHuJobs software development as well as the technical implementation of service components",
},
]

const delay = [0, 75, 100, 150, 200, 300, 500, 700, 1000];
const target = ref(null);
const observer = shallowRef();

onMounted(() => {
  observer.value = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        entry.target.classList.toggle(
          "lg:[&[show=true]]:opacity-100",
          entry.isIntersecting
        );
        entry.target.classList.toggle(
          "lg:[&[show=true]]:translate-x-0",
          entry.isIntersecting
        );
        entry.target.classList.toggle(
          "lg:[&[show=true]]:translate-y-0",
          entry.isIntersecting
        );
        if (entry.isIntersecting) {
          observer.value.unobserve(entry.target);
          return entry.target;
        }
      });
    },
    {
      threshold: 0.1,
    }
  );
  target.value.forEach((selection) => {
    observer.value.observe(selection);
  });
});
</script>

<template>
  <section class="flex flex-col overflow-hidden" id="team">
    <div class="flex flex-col items-center">
      <h2 show="true" class="mt-10 self-center text-lg font-medium leading-[18px] dark:text-white lg:mt-[90px]">
        OUR TEAM
      </h2>
      <h2 show="true"
        class="mt-[34px] self-center rounded-[36px] bg-primary-lite px-3 py-2 text-center text-base font-black leading-5 text-white xs:px-8 xs:text-lg lg:px-4 3xl:px-8 lg:py-2 3xl:py-4 lg:text-2xl 3xl:text-3xl lg:leading-[18px]">
        Here are some of our core management team
      </h2>
      <!-- <p show="true"
        class="mt-[34px] max-w-[900px] text-center text-base font-light leading-[30px] dark:text-HahuGray/4 xs:text-lg">
        Highly professional and capable of running your business across all
        digital channels.
      </p> -->
    </div>

    <div
      class="mt-11 flex flex-wrap items-center justify-center gap-x-0 gap-y-6 md:gap-x-4 lg:gap-x-6 lg:gap-y-6 4xl:gap-x-16 4xl:gap-y-16">
      <div v-for="(person, i) in team" show="true" ref="target"
        class="self-center lg:duration-500 lg:opacity-0 rounded-md bg-white hover:shadow-full overflow-hidden dark:bg-HahuGray1"
        :class="`lg:delay-${delay[i]}`">
        <div class="relative mt-5 flex flex-row justify-center">
          <img class="self-center rounded-full" :src="person.img" alt="team" />
          <img :src="person.icon" class="absolute top-[-5px] right-5 w-6" alt="personIcon" />
        </div>
        <h2 class="mt-1 items-center text-center text-2xl font-black leading-[38px] dark:text-HahuGray/4">
          {{ person.name }}
        </h2>
        <h2 class="mt-2 text-center text-lg font-medium leading-7 text-primary">
          {{ person.pos }}
        </h2>
        <p
          class="mx-8 mt-6 mb-20 max-w-[260px] 3xl:max-w-[295px] text-center text-base font-medium leading-6 dark:text-HahuGray3">
          {{ person.prov }}
        </p>
      </div>

    </div>

    <div
      class="mt-11 flex flex-wrap items-center justify-center gap-x-0 gap-y-6 md:gap-x-4 lg:gap-x-6 lg:gap-y-6 4xl:gap-x-16 4xl:gap-y-16">

      <div v-for="(person, i) in team2" show="true" ref="target"
        class="group lg:duration-500 lg:opacity-0 rounded-md bg-white hover:shadow-full overflow-hidden dark:bg-HahuGray1 mb-2"
        :class="`lg:delay-${delay[i]}`">
        <div class="relative mt-5 flex flex-row justify-center">
          <img class="self-center rounded-full" :src="person.img" alt="team" />
          <img :src="person.icon" class="absolute top-[-5px] right-5 w-6" alt="personIcon" />
        </div>
        <h2 class="mt-1 items-center text-center text-2xl font-black leading-[38px] dark:text-HahuGray/4">
          {{ person.name }}
        </h2>
        <h2 class="mt-2 text-center text-lg font-medium leading-7 text-primary">
          {{ person.pos }}
        </h2>
        <p
          class="mx-8 mt-6 mb-20 max-w-[240px] 3xl:max-w-[295px] text-center text-base font-medium leading-6 dark:text-HahuGray3 line-clamp-4 group-hover:line-clamp-none">
          {{ person.prov }}
        </p>
      </div>
    </div>
  </section>
</template>

<style scoped>
</style>
