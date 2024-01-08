<template>
  <button
    :class="{
      'bg-[#2f80ed]': props.color === 'blue',
      'hover:bg-[#1d51b0]': props.color === 'blue',
      'bg-[#f8b76b]': props.color === 'orange' && props.isMenuOpen,
      'text-[#f8b76b]': props.color === 'orange' && !props.isMenuOpen,
      'hover:bg-[#e36013]': props.color === 'orange' && props.isMenuOpen,
      'bg-[#8785ff]': props.color === 'purple' && props.isMenuOpen,
      'text-[#8785ff]': props.color === 'purple' && !props.isMenuOpen,
      'hover:bg-[#5a3dee]': props.color === 'purple' && props.isMenuOpen,
      'bg-light': !props.isMenuOpen && !props.isStatic,
      'text-light': props.isMenuOpen,
      'hover:bg-[#adadad]': !props.isMenuOpen && !props.isStatic,
    }"
    class="rounded-full p-2 transition-colors duration-100"
  >
    <slot>
      <ThunderIcon size="2em" color="#fff" />
    </slot>
  </button>
</template>
<script setup>
import ThunderIcon from "./icons/ThunderIcon.vue";

const props = defineProps({
  color: {
    type: String,
    default: "blue",
  },
  isMenuOpen: {
    type: Boolean,
    default: false,
  },
  isStatic: {
    type: Boolean,
    default: false,
  },
});
</script>
<style lang=""></style>
