<script setup>
import Message from './Message.vue';
defineProps({
  channelId: Number
});
</script>
<script>
export default {
  data() {
    return {
    }
  },
  computed: {
    channel() {
      return window.getChannel(this.channelId);
    }
  }
}
</script>
<template>
  <main class="h-screen left-80 relative">
    <header
      class="fixed top-0 left-80 right-0 p-4 font-bold bg-zinc-800 text-white text-lg shadow-sm shadow-black"
    >
      <h2>
        <i class="fas fa-hashtag text-zinc-500"></i>
        &nbsp;{{ channel.name }}
      </h2>
    </header>
    <ul class="pb-20 flex flex-col gap-2 justify-end min-h-screen">
      <Message v-for="message in channel.messages" :message="message"></Message>
    </ul>
    <div
      class="fixed bg-zinc-600 text-zinc-200 translate-x-4 left-80 right-8 bottom-4 h-12 align-middle justify-between rounded-lg shadow-sm"
    >
      <i class="fa fa-plus-circle absolute p-4 cursor-pointer hover:text-white"></i>
      <input
        class="bg-zinc-600 text-white w-full h-12 align-middle justify-between rounded-lg pl-12 shadow-sm focus:outline-none"
        :placeholder="`Envoyer un message dans #${channel.name} :`"
      />
    </div>
  </main>
</template>