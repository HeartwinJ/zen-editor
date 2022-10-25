<script setup lang="ts">
import { onMounted, reactive, ref, watch } from "vue";

const contentDiv = ref<any>(null);

const data = reactive({
  title: "",
  content: "",
});

watch(data, (val) => {
  localStorage.setItem("title", val.title),
    localStorage.setItem("content", val.content);
});

onMounted(() => {
  data.title = localStorage.getItem("title") || "";
  data.content = localStorage.getItem("content") || "";

  setTimeout(() => {
    contentDiv.value.innerText = data.content;
  }, 100);
});
</script>

<template>
  <div class="flex h-screen w-screen justify-center bg-stone-900">
    <div class="flex h-full w-full max-w-2xl flex-col gap-4 py-4">
      <input
        type="text"
        placeholder="Title"
        class="bg-transparent text-4xl text-stone-200 outline-none placeholder:italic placeholder:text-stone-500"
        v-model="data.title"
      />
      <div
        ref="contentDiv"
        class="relative bg-transparent text-xl text-stone-200 outline-none"
        placeholder="content"
        contenteditable
        @input="(e: any) => (data.content = e.target.innerText)"
      ></div>
    </div>
  </div>
</template>
