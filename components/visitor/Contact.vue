<script setup>
import { Form, Field, useForm } from "vee-validate";
import Branch from "@/assets/svg/Branch.svg?url";
import Email from "@/assets/svg/Email.svg?url";
import Phone from "@/assets/svg/Phone.svg?url";
import Office from "@/assets/svg/Office.svg?url";
import {
  TransitionRoot,
  TransitionChild,
  Dialog,
  DialogPanel,
  DialogTitle,
} from '@headlessui/vue'

import {
  LMap,
  LTileLayer,
  LMarker,
  LControlScale,
  LTooltip,
  LControlZoom,
  LPopup,
  LIcon,
} from "@vue-leaflet/vue-leaflet";

import "leaflet/dist/leaflet.css";

const zoom = ref(18)
const isOpen = ref(false)

function closeModal() {
  isOpen.value = false
}
function openModal() {
  isOpen.value = true
}


const item = reactive({});
const branchs = [
  { name: "Bahr Dar", Phone: "+251-5-85-56-67-77" },
  { name: "Bole lemi", Phone: " +251-1-18-60-07-66" },
  { name: "Adama", Phone: "+251-2-22-12-92-51" },
  { name: "Debire Birhan", Phone: "+251-1-16-73-11-20" },
  { name: "Dire Dawa", Phone: "+251-2-58-90-90-18" },
  { name: "Kombolcha", Phone: "+251-3-33-51-64-35" },
  { name: "Hawassa", Phone: "+251-4-68-21-23-37" },
  // { name: "Mekelle", Phone: "" },
  // { name: "Yirgalem", Phone: "Comming soon!" },
  // { name: "Bure", Phone: "Comming soon" },
  // { name: "Bulbula", Phone: "Comming soon" },
];

const { handleSubmit } = useForm({});
const submit = handleSubmit(async (values) => {
  const { data: api } = await useFetch('https://formspree.io/f/mgeqwwwe', { method: 'post', body: values })
  console.log('api : ', api.value.ok);
  if (api.value.ok) {
    openModal()
  } else {
    alert('Message submission failed')
  }
});

const delay = [0, 75, 100, 150, 200, 300, 500, 700, 1000];
</script>

<template>
  <section class="mt-10 flex flex-col" id="contact">
    <div class="mb-20 flex flex-col items-center">
      <h2 show="true" class="mt-10 self-center text-lg font-medium leading-[18px] dark:text-white lg:mt-[90px]">
        Contact
      </h2>
      <h2 show="true"
        class="mt-[34px] self-center rounded-[36px] bg-primary-lite px-3 py-2 text-center text-base font-black leading-5 text-white xs:px-8 xs:text-lg lg:px-4 3xl:px-8 lg:py-2 3xl:py-4 lg:text-2xl 3xl:text-3xl lg:leading-[18px]">
        We would love to hear from you!
      </h2>
      <p show="true"
        class="mt-[34px] max-w-[900px] text-center text-base font-light leading-[30px] dark:text-HahuGray/4 xs:text-lg">
        Please fill out the form below to reach our communications department
        for any enquiries you may have, our doors are open for everyone
      </p>
    </div>
    <div class="flex flex-col 2xl:flex-row 2xl:space-x-[106px]">
      <div class="mb-[58px] flex-1">
        <div class="mt-6 flex flex-col justify-around sm:flex-row">
          <div show="true" class="flex flex-row flex-wrap items-baseline">
            <img :src="Email" alt="email" />
            <div class="ml-[15px] flex flex-col">
              <h2 class="text-xl font-bold leading-[38px] text-primary">
                Email
              </h2>
              <h4 class="text-lg font-normal leading-[30px] text-HahuGray2 duration-500 ease-in dark:text-HahuGray/4">
                info@hahu.jobs
              </h4>
            </div>
          </div>

          <div show="true" class="flex flex-row flex-wrap items-baseline">
            <img :src="Phone" alt="phone" />
            <div class="ml-[15px] flex flex-col">
              <h2 class="text-xl font-bold leading-[38px] text-primary">
                Phone
              </h2>
              <h4 class="text-lg font-normal leading-[30px] text-HahuGray2 duration-500 ease-in dark:text-HahuGray/4">
                +251-11 822 1001
                <br />
                +251-11 822 1002
              </h4>
            </div>
          </div>

          <div show="true" class="flex flex-row flex-wrap items-baseline">
            <img :src="Office" alt="office" />
            <div class="ml-[15px] flex flex-col">
              <h2 class="text-xl font-bold leading-[38px] text-primary">
                Office
              </h2>
              <h4 class="text-lg font-normal leading-[30px] text-HahuGray2 duration-500 ease-in dark:text-HahuGray/4">
                Bole, Behind DH geda tower <br />Afomi Building 3rd floor
                <br />Addis Ababa
              </h4>
            </div>
          </div>
        </div>
        <div class="mt-16 w-full h-96">
          <l-map v-model="zoom" v-model:zoom="zoom" :maxZoom="18" :options="{ zoomControl: false }"
            :center="[8.9894, 38.786]" class="z-0 w-10/12 h-20">
            <l-tile-layer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"></l-tile-layer>
            <l-control-zoom position="bottomright"></l-control-zoom>
            <l-control-scale position="topright" :imperial="true" :metric="false"></l-control-scale>
            <l-marker :lat-lng="[8.9894, 38.786]">
              <l-tooltip> Hahu Jobs </l-tooltip>
              <l-popup>
                <div class="w-28 h-28">
                  <div class="flex justify-center font-body font-medium text-sm text-primary">
                    Hahu Jobs
                  </div>
                  <div class="flex flex-col justify-center mt-3">
                    <img src="/images/Hahu-031.png" class="w-full" />
                    <img src="/images/Hahu_logo2.png" class="w-full mt-3" />
                  </div>
                  <div class="mt-5 text-primary">
                    <a href="#" class="hover:underline hover:italic font-body text-sm">www.HahuJobs.io</a>
                  </div>
                </div>
              </l-popup>
              <l-icon icon-url="/icons/favicon.ico" :icon-size="[20, 20]" />
            </l-marker>
          </l-map>
        </div>
        <div class="mt-16 flex flex-row flex-wrap items-baseline">
          <img :src="Branch" alt="branch" />
          <div class="ml-[15px] flex flex-col">
            <h2 class="text-xl font-bold leading-[38px] text-primary">
              Branch
            </h2>
            <ul
              class="mt-8 grid w-full grid-cols-2 items-center justify-items-end gap-x-4 gap-y-9 xs:gap-x-28 md:grid-cols-3 lg:gap-x-16 3xl:gap-x-28">
              <li show="true" class="flex flex-col gap-y-1" v-for="(branch, i) in branchs">
                <h2 class="text-xl font-semibold leading-6 text-HahuGray1 duration-500 ease-in dark:text-white">
                  {{ branch.name }}
                </h2>
                <h3
                  class="sm:ml-2 text-base font-normal leading-8 text-gray-500 duration-500 ease-in dark:text-HahuGray4">
                  {{ branch.Phone }}
                </h3>
              </li>
            </ul>
          </div>
        </div>
      </div>
      <div class="sm:flex-1 flex sm:justify-center">

        <form @submit.prevent="submit" show="true"
          class="flex pb-10 lg:pb-5 max-h-[915px] w-full sm:w-10/12 lg:w-full 3xl:w-10/12 flex-col rounded-md bg-white pt-11 px-2 ease-in dark:bg-HahuGray1 sm:px-3 md:px-10 lg:px-20 xl:px-24">
          <InputsHtextfield rules="required" v-model="item.name" type="text" name="name" :placeholder="$t('your_name')"
            class="dark:text-white" placeholderStyle="text-HahuGray2">
            <template v-slot:label>
              <div class="mb-5 text-lg font-medium leading-6 text-gray-800 dark:text-white">
                {{ $t("name") }}
              </div>
            </template>
          </InputsHtextfield>
          <InputsHtextfield rules="required|ethiopian_phone_number" v-model="item.phone" type="text" name="phone"
            placeholder="09..." placeholderStyle="text-HahuGray2" class="dark:text-white"><template v-slot:label>
              <div class="mb-5 text-lg font-medium leading-6 text-gray-800 dark:text-white">
                {{ $t("phone_number") }}
              </div>
            </template></InputsHtextfield>
          <InputsHtextfield rules="required|email" v-model="item.email" type="text" name="email"
            :placeholder="$t('your_email')" placeholderStyle="text-HahuGray2 dark:text-white" class="dark:text-white">
            <template v-slot:label>
              <div class="mb-5 text-lg font-medium leading-6 text-gray-800 dark:text-white">
                {{ $t("email") }}
              </div>
            </template>
          </InputsHtextfield>
          <InputsHtextarea type="text" rules="required" v-model="item.message" :placeholder="$t('your_message_here')"
            inputClass="dark:text-white" placeholderStyle="placeholder-HahuGray1  dark:placeholder-white"
            :label="$t('message')"
            labelClass="font-medium text-gray-800 text-lg leading-6 dark:text-white duration-500 ease-in mb-5"
            name="message" />

          <button type="submit"
            class="mt-9 w-full rounded-md bg-primary py-3 text-xl font-medium leading-7 text-whitePrimary">
            {{ $t('send') }}
          </button>
          <TransitionRoot appear :show="isOpen" as="template">
            <Dialog as="div" @close="closeModal" class="relative z-10">
              <TransitionChild as="template" enter="duration-300 ease-out" enter-from="opacity-0" enter-to="opacity-100"
                leave="duration-200 ease-in" leave-from="opacity-100" leave-to="opacity-0">
                <div class="fixed inset-0 bg-black bg-opacity-25" />
              </TransitionChild>

              <div class="fixed inset-0 overflow-y-auto">
                <div class="flex min-h-full items-center justify-center p-4 text-center">
                  <TransitionChild as="template" enter="duration-300 ease-out" enter-from="opacity-0 scale-95"
                    enter-to="opacity-100 scale-100" leave="duration-200 ease-in" leave-from="opacity-100 scale-100"
                    leave-to="opacity-0 scale-95">
                    <DialogPanel
                      class="w-full max-w-md transform overflow-hidden rounded-2xl bg-white dark:bg-LightDark p-6 text-left align-middle shadow-xl transition-all">
                      <DialogTitle as="h3" class="text-lg font-medium leading-6 text-primary">
                        Message successful sent.
                      </DialogTitle>
                      <div class="mt-2">
                        <p class="text-sm text-gray-500 dark:text-white">
                          Your Message has been successfully submitted. We will contact you soon.
                        </p>
                      </div>

                      <div class="mt-4">
                        <button type="button"
                          class="inline-flex justify-center rounded-md border border-transparent bg-green-100 px-4 py-2 text-sm font-medium text-primary hover:bg-green-200 focus:outline-none focus-visible:ring-2 focus-visible:ring-green-500 focus-visible:ring-offset-2"
                          @click="closeModal">
                          Got it, thanks!
                        </button>
                      </div>
                    </DialogPanel>
                  </TransitionChild>
                </div>
              </div>
            </Dialog>
          </TransitionRoot>
        </form>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
</style>
