<script setup>
    defineProps(["itemTitle", "isActive"]);
    defineEmits(["change-active"])

</script>

<template>
    <li class="w-[120px] transition-all cursor-pointer p-2 mr-2" v-bind:class="{'bg-neutral':isActive, 'text-white':isActive}" @click="$emit('change-active', index)">
        {{itemTitle}}
    </li>
</template>