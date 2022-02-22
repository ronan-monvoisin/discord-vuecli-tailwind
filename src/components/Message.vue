<script setup>
defineProps({
  message: Object
});
</script>
<script>
export default {
  data() {
    return {
      test: ""
    }
  },
  computed: {
    user() {
      return window.getUser(this.message.authorId);
    },
    channel() {
      return window.getChannel(this.channelId);
    }
  }
}
</script>
<template>
  <li class="w-full flex flex-row px-8">
    <figure class="float-left h-12 w-12">{{ message.authorId }}</figure>
    <div>
      <div class="font-semibold mr-2">
        {{ user.name }}
        <span class="font-light text-xs text-zinc-400">{{ message.date }}</span>
      </div>
      {{ message.content }}
    </div>
  </li>
</template>