<template>
  <div
    class="text-sm md:min-h-[600px]"
    :class="{ 'flex flex-col items-center justify-center gap-y-2': isLoading }"
  >
    <template v-if="isLoading">
      <div class="text-secondary">
        <LoadingIcon size="3.5em" />
      </div>
      <div class="font-semibold text-secondary">Loading Chats ...</div>
    </template>
    <div
      v-else-if="typeof choosenChat === 'boolean' && !choosenChat"
      class="px-4 py-3"
    >
      <input
        type="text"
        class="mb-4 w-full rounded-md border border-black px-2 py-1 focus:outline-none"
        placeholder="Search"
      />
      <div>
        <div v-for="(chats, index) in chatData" class="group relative">
          <div
            class="pointer-events-none absolute left-0 top-0 z-50 h-full w-full opacity-20 transition-all duration-100 group-hover:bg-black"
          ></div>
          <chat-list
            @click="selectChat(index)"
            class="cursor-pointer border-b border-black hover:bg-blend-darken"
            :chats="chats"
          >
          </chat-list>
        </div>
      </div>
    </div>
    <div v-else class="flex flex-col">
      <!-- header part -->
      <div class="flex items-center gap-x-4 px-4 pt-3">
        <button
          class="transition-colors duration-100 hover:bg-secondary hover:bg-opacity-10"
          @click="choosenChat = false"
        >
          <BackIcon size="1.5em" />
        </button>
        <div class="flex-1">
          <p class="text-lg font-medium leading-6 text-primary">
            {{ chatData[choosenChat].title }}
          </p>
          <p class="text-sm text-secondary">3 Participant</p>
        </div>
        <button
          class="transition-colors duration-100 hover:bg-secondary hover:bg-opacity-10"
          @click="close"
        >
          <CloseIcon size="1.5em" />
        </button>
      </div>
      <!-- end header part -->
      <hr class="my-3 h-px border-0 bg-gray-200" />
      <!-- body part -->
      <div class="mb-2 flex-1 overflow-auto px-4 py-3">
        <div
          v-for="(n, index) in 3"
          class="flex flex-col"
          :ref="(el) => itemRefs.push(el)"
        >
          <input
            type="checkbox"
            :id="`label-${index}`"
            class="popper-toggler hidden"
            @change="isPopperChecked"
          />
          <p class="mb-1 text-right">You</p>
          <div class="flex justify-end gap-x-2">
            <div
              class="popper-content min-w-32 overflow-hidden rounded-md border border-secondary bg-white"
            >
              <button
                class="w-full border-b border-gray-500 p-2 text-start text-primary transition-colors duration-100 hover:bg-primary hover:text-white"
              >
                Edit
              </button>
              <button
                class="w-full p-2 text-start text-red-500 transition-colors duration-100 hover:bg-red-500 hover:text-white"
              >
                Delete
              </button>
            </div>
            <div class="flex">
              <label :for="`label-${index}`" class="h-fit cursor-pointer">
                <OptionIcon size="1.5em" class="popper-button text-secondary" />
              </label>
            </div>
            <div class="flex flex-col rounded-md bg-blue-200 p-2 text-gray-600">
              <p class="mb-2 max-w-[30ch] md:max-w-[40ch]">
                Lorem ipsum, dolor sit amet consectetur adipisicing elit.
                Tempore sapiente labore rem, ab doloremque minus expedita
                beatae! Laboriosam, numquam perspiciatis.
              </p>
              <p class="text-xs">19:43</p>
            </div>
          </div>
        </div>
      </div>
      <!-- end body part -->
      <!-- footer part -->
      <div class="flex gap-x-3 px-4 pb-3">
        <input
          type="text"
          class="flex-1 rounded-md border border-secondary p-2 focus:outline-none"
          placeholder="Type a new message"
        />
        <button class="rounded bg-primary px-4 py-2 text-white">Send</button>
      </div>
      <!-- end footer part -->
    </div>
  </div>
</template>
<script setup>
import { ref, onMounted, onUpdated, onBeforeUpdate } from "vue";
import { createPopper } from "@popperjs/core";

import ChatList from "./MessengerChatList.vue";
import chatData from "@/mixins/chat-data.mjs";
import { delay } from "@/mixins/ultilities.mjs";

import CloseIcon from "./icons/CloseIcon.vue";
import BackIcon from "./icons/BackIcon.vue";
import OptionIcon from "./icons/OptionIcon.vue";
import LoadingIcon from "./icons/LoadingIcon.vue";

const emit = defineEmits(["close"]);

const choosenChat = ref(false);
const isLoading = ref(true);
const itemRefs = ref([]);

onMounted(async () => {
  await delay(1500);
  isLoading.value = false;
});

onUpdated(async () => {
  if (typeof choosenChat.value === "number") {
    itemRefs.value.forEach((item) => {
      const popperButton = item.querySelector(".popper-button");
      const popperContent = item.querySelector(".popper-content");

      createPopper(popperButton, popperContent, { placement: "bottom-end" });
    });
  } else {
    // check if theres poper intance, if its exist delete them
  }
});
onBeforeUpdate(() => {
  if (typeof choosenChat.value === "number") {
    itemRefs.value = [];
  }
});
function selectChat(index) {
  choosenChat.value = index;
}

function close() {
  emit("close");
}

function isPopperChecked(e) {
  // WIP (work in progress, toggle the popper content outside of the content area)
  // const toggler = e.target;
  // const parentElement = toggler.parentElement;
  // const popperContent = parentElement.querySelector(".popper-content");
  // if (e.target.checked) {
  //   popperContent.style.zIndex = 100;
  //   const overlayElement = document.createElement("div");
  //   overlayElement.style.position = "fixed";
  //   overlayElement.style.left = 0;
  //   overlayElement.style.top = 0;
  //   overlayElement.style.height = "100%";
  //   overlayElement.style.width = "100%";
  //   overlayElement.style.opacity = 0;
  //   overlayElement.addEventListener("click", function clickListener() {
  //     console.log("click");
  //     overlayElement.removeEventListener("click", clickListener);
  //     popperContent.style.zIndex = 0;
  //   });
  //   document.querySelector('body').appendChild(overlayElement);
  // } else {
  //   popperContent.style.zIndex = 0;
  // }
}
</script>
<style lang="scss">
.popper-toggler {
  &:not(:checked) {
    + p {
      + div {
        .popper-content {
          display: none;
        }
      }
    }
  }
}
</style>
