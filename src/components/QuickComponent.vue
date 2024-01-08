<template>
  <div class="fixed bottom-4 right-8 z-50">
    <div class="relative flex flex-row-reverse gap-x-4">
      <div
        class="absolute bottom-14 right-0 w-72 rounded-md bg-white opacity-0 shadow-lg sm:w-96 lg:w-[35rem]"
        id="feature-wrapper"
      >
        <MessengerComponent
          @close="toggleChildMenu('message')"
          v-if="messageDisplay"
        />
      </div>
      <quick-button
        @click="toggleMenu"
        :isStatic="true"
        :class="{ hidden: isMessageOpen || isTaskOpen }"
      >
        <ThunderIcon size="1.5em" color="#fff" />
      </quick-button>
      <div class="flex hidden gap-x-4" ref="menuContainer">
        <quick-button
          @click="toggleChildMenu('message')"
          color="purple"
          :isMenuOpen="isMessageOpen"
          :class="{ 'order-2': isMessageOpen }"
          class="fadeIn"
        >
          <BubbleChatIcon size="1.5em" />
        </quick-button>
        <quick-button
          @click="toggleChildMenu('task')"
          color="orange"
          :isMenuOpen="isTaskOpen"
          :class="{ 'order-2': isTaskOpen }"
          class="fadeIn"
        >
          <BookIcon size="1.5em" />
        </quick-button>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, watch } from "vue";
import { gsap } from "gsap";
import ThunderIcon from "./icons/ThunderIcon.vue";
import BubbleChatIcon from "./icons/BubbleChatIcon.vue";
import BookIcon from "./icons/BookIcon.vue";
import QuickButton from "./QuickButton.vue";

import MessengerComponent from "./MessengerComponent.vue";

const isMessageOpen = ref(false);
const messageDisplay = ref(false);
const isTaskOpen = ref(false);
const menuContainer = ref(null);

watch(isMessageOpen, function (newValue) {
  if (!newValue) {
    gsap.fromTo(
      "#feature-wrapper",
      {
        display: "block",
        yPercent: 0,
        opacity: 1,
      },
      {
        display: "none",
        yPercent: 10,
        opacity: 0,
        onComplete() {
          messageDisplay.value = !messageDisplay.value;
        },
      },
    );
  } else {
    messageDisplay.value = !messageDisplay.value;
    gsap.fromTo(
      "#feature-wrapper",
      {
        display: "none",
        yPercent: 10,
        opacity: 0,
      },
      {
        display: "block",
        yPercent: 0,
        opacity: 1,
      },
    );
  }
});

function toggleMenu() {
  if (menuContainer.value.classList.contains("hidden")) {
    menuContainer.value.classList.toggle("hidden");
  } else {
    menuContainer.value.classList.add("fadeOut");
    menuContainer.value.addEventListener(
      "animationend",
      function onAnimationEnd() {
        this.removeEventListener("animationend", onAnimationEnd);
        this.classList.toggle("hidden");
        this.classList.remove("fadeOut");
      },
    );
  }
}

function toggleChildMenu(childMenu) {
  if (childMenu === "message") {
    isTaskOpen.value = false;
    isMessageOpen.value = !isMessageOpen.value;
  }
  if (childMenu === "task") {
    isMessageOpen.value = false;
    isTaskOpen.value = !isTaskOpen.value;
  }
}
</script>
<style lang="scss">
div {
  &:not(.hidden) {
    .fadeIn {
      animation-name: fadeIn;
      animation-duration: 0.3s;
    }
  }
}

.fadeOut {
  animation-name: fadeOut;
  animation-duration: 0.3s;
}

@keyframes fadeIn {
  0% {
    transform: translateX(10px);
    opacity: 0;
  }
  100% {
    transform: translateX(0);
    opacity: 1;
  }
}
@keyframes fadeOut {
  to {
    transform: translateX(10px);
    opacity: 0;
  }
}
</style>
