<template>
  <div>
    <Quick />
    <aside
      class="fixed h-full border-r border-white bg-dark"
      :class="{ 'w-44': windowWidth > 576, 'w-12': windowWidth < 577 }"
    ></aside>
    <div
      class="flex min-h-screen flex-col"
      :class="{ 'ml-44': windowWidth > 576, 'ml-12': windowWidth < 577 }"
    >
      <header class="bg-secondary p-4">asd</header>
      <main class="flex-1 p-4">
        <div class="rounded-md bg-white p-4">
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Ab eligendi
            vitae illo hic quidem maiores adipisci sint, qui accusantium quo
            blanditiis aperiam doloremque asperiores quasi velit neque eos
            dolore quod. Minima, quis dolorum reprehenderit incidunt ipsa
            repellat possimus quod, eligendi ducimus nisi adipisci libero.
            Facere tenetur perferendis, deserunt consequatur nisi temporibus.
            Porro ut illum quod, perferendis tempore dolorum. Eius explicabo
            quisquam harum, fugiat aliquid blanditiis corporis officia beatae.
            Culpa quia ullam, voluptates impedit expedita sint, architecto ea
            possimus reprehenderit optio laboriosam officia consequatur
            adipisci. Minima omnis alias asperiores. Ducimus rem aperiam
            assumenda! Voluptates magnam expedita ab distinctio corporis,
            molestias quia.
          </p>
        </div>
      </main>
    </div>
  </div>
</template>
<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";
import Quick from "@/components/QuickComponent.vue";

const windowWidth = ref(0);

onMounted(() => {
  windowWidth.value = window.innerWidth;
  window.addEventListener("resize", resizeHandler);
});

onBeforeUnmount(() => {
  window.removeEventListener("resize", resizeHandler);
});

function resizeHandler(e) {
  windowWidth.value = e.target.innerWidth;
}
</script>
<style lang=""></style>
