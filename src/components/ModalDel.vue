<script setup>
    defineProps(['switchModal']);
    defineEmits(['del-container-item', 'close-modal'])
</script>

<template>
  <div
    class="fixed top-0 left-0 min-h-screen w-full z-10 transition-all flex items-center justify-center"
    v-bind:class="{ visibility: switchModal, hidden: !switchModal }"
  >
    <div
      class="z-30 bg-base-300 p-4 rounded-md shadow-md w-96 transition-all flex flex-col gap-4"
    >
      <h1 class="transition-all self-center">Modal Window Title</h1>
      <p class="transition-all">
        Lorem, ipsum dolor sit amet consectetur adipisicing elit. Qui,
        perferendis! <br />
        Are you sure ?
      </p>
      <div class="transition-all self-end flex items-center gap-4">
        <button
          class="transition-all btn-outline btn btn-success"
          @click="$emit('del-container-item')"
        >
          Yes
        </button>
        <button
          class="transition-all btn-outline btn btn-error"
          @click="$emit('close-modal')"
        >
          Cancel
        </button>
      </div>
    </div>
    <div
      class="absolute top-0 left-0 min-h-screen w-full bg-black opacity-50 z-20 transition-all"
      @click="$emit('close-modal')"
    ></div>
  </div>
</template>