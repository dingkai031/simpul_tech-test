<template>
  <div class="flex">
    <div class="p-2 flex items-center justify-center relative min-w-20">
      <div v-if="type === 'group'">
        <div
          class="absolute inline-flex items-center justify-center w-10 h-10 overflow-hidden bg-secondary rounded-full p-2"
        >
          <span class="text-gray-600">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="1.5em"
              height="1.5em"
              viewBox="0 0 24 24"
            >
              <path
                fill="currentColor"
                d="M9.775 12q-.9 0-1.5-.675T7.8 9.75l.325-2.45q.2-1.425 1.3-2.363T12 4q1.475 0 2.575.938t1.3 2.362l.325 2.45q.125.9-.475 1.575t-1.5.675h-4.45Zm0-2h4.45L13.9 7.6q-.1-.7-.637-1.15T12 6q-.725 0-1.263.45T10.1 7.6L9.775 10ZM12 10ZM4 20v-2.8q0-.85.438-1.563T5.6 14.55q1.55-.775 3.15-1.163T12 13q1.65 0 3.25.388t3.15 1.162q.725.375 1.163 1.088T20 17.2V20H4Zm2-2h12v-.8q0-.275-.138-.5t-.362-.35q-1.35-.675-2.725-1.012T12 15q-1.4 0-2.775.338T6.5 16.35q-.225.125-.363.35T6 17.2v.8Zm6 0Z"
              />
            </svg>
          </span>
        </div>
        <div
          class="ml-6 relative inline-flex items-center justify-center w-10 h-10 overflow-hidden bg-primary rounded-full p-2"
        >
          <span class="text-white">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="1.5em"
              height="1.5em"
              viewBox="0 0 24 24"
            >
              <path
                fill="currentColor"
                d="M9.775 12q-.9 0-1.5-.675T7.8 9.75l.325-2.45q.2-1.425 1.3-2.363T12 4q1.475 0 2.575.938t1.3 2.362l.325 2.45q.125.9-.475 1.575t-1.5.675h-4.45Zm0-2h4.45L13.9 7.6q-.1-.7-.637-1.15T12 6q-.725 0-1.263.45T10.1 7.6L9.775 10ZM12 10ZM4 20v-2.8q0-.85.438-1.563T5.6 14.55q1.55-.775 3.15-1.163T12 13q1.65 0 3.25.388t3.15 1.162q.725.375 1.163 1.088T20 17.2V20H4Zm2-2h12v-.8q0-.275-.138-.5t-.362-.35q-1.35-.675-2.725-1.012T12 15q-1.4 0-2.775.338T6.5 16.35q-.225.125-.363.35T6 17.2v.8Zm6 0Z"
              />
            </svg>
          </span>
        </div>
      </div>
      <div v-if="type === 'user'">
        <div
          class="relative inline-flex items-center justify-center w-10 h-10 overflow-hidden bg-gray-100 rounded-full"
        >
          <span class="font-medium text-gray-600 uppercase">{{
            latestMessage.name[0]
          }}</span>
        </div>
      </div>
    </div>
    <div class="flex flex-col p-2 flex-1">
      <div class="flex gap-x-8 mb-2 justify-between">
        <p class="text-primary font-bold text-lg line leading-5">
          {{ title }}
        </p>
        <p class="whitespace-nowrap text-secondary text-sm">
          {{ new Date(latestMessage.time).toLocaleString() }}
        </p>
      </div>
      <div>
        <p class="capitalize font-bold text-secondary">
          {{ latestMessage.name }} :
        </p>
        <p class="text-secondary">{{ latestMessage.message }}</p>
      </div>
    </div>
  </div>
</template>
<script setup>
const props = defineProps(["chats"]);
const { title, type, chatList } = props.chats;

let sortedChatList = chatList.sort((a, b) => a.time - b.time);
const latestMessage = sortedChatList[sortedChatList.length - 1];
</script>
<style lang=""></style>
