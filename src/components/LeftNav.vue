<script setup>
import Icone from './Icone.vue';
defineProps({
  //userId: int
});
 </script>
<script>
export default {
  emits: ['newServ'],
  data() {
    return {
    }
  },
  methods: {
    pushServ(serverId) {
      this.$emit('newServ', serverId);
    }
  },
  computed: {
    servers(){
      return window.getServers()
      }
  }
}
</script>
<template>
    <nav class="flex flex-col flex-shrink-0 w-20 m-0 bg-zinc-900 h-screen text-white">
      <Icone v-for="server in servers" :server="server" @click="pushServ(server.id)" />
    </nav>
  <slot></slot>
</template>
