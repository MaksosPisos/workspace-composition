<script setup>
defineProps(["switchModal"]);
defineEmits(["close-modal"]);
</script>

<template>
  <div
    class="fixed top-0 left-0 min-h-screen w-full z-10 transition-all flex items-center justify-center"
    v-bind:class="{ visibility: switchModal, hidden: !switchModal }"
  >
    <div
      class="z-30 bg-base-300 p-4 rounded-md shadow-md w-[500px] transition-all flex flex-col gap-4"
    >
      <h1 class="self-center">Выбери тип контента</h1>
      <div class="flex flex-col gap-4">
        <div class="flex gap-2 items-start">
          <input
            type="checkbox"
            checked="checked"
            class="checkbox checkbox-md"
          />
          <h3>Текст</h3>
          <textarea
            name=""
            id=""
            cols="30"
            rows="10"
            class="p-4 rounded-md border-2 border-base-200"
          >
Default text
                </textarea
          >
        </div>
        <div class="flex gap-2 items-center">
          <input
            type="checkbox"
            checked="checked"
            class="checkbox checkbox-md"
          />
          <h3>Изображение</h3>
          <input type="file" name="" id="">
        </div>
        <div class="flex gap-2 items-center">
          <input
            type="checkbox"
            checked="checked"
            class="checkbox checkbox-md"
          />
          <h3 class="min-w-[108px]">Видео</h3>
          <input type="file" name="" id="">
        </div>
        
      </div>
    </div>
    <div
      class="absolute top-0 left-0 min-h-screen w-full bg-black opacity-50 z-20 transition-all"
      @click="$emit('close-modal')"
    ></div>
  </div>
</template>
