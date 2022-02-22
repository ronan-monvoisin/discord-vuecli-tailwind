<script setup>
defineProps({
    server: Object
})
</script>

<template>
    <div class="icon group">
        <i class="text-2xl" :class="server.icon" v-html="server.content"></i>
        <span class="icon-tooltip group-hover:scale-100">{{ server.name }}</span>
    </div>
</template>