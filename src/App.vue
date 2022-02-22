<script setup>
import LeftNav from './components/LeftNav.vue';
import LeftChan from './components/LeftChan.vue';
import Discussion from './components/Discussion.vue';
  </script>
<script>
export default {
  data() {
    return {
      userId: 1,
      serverId: 1,
      channelId: 1
    }
  },
  methods: {
    setServer(id) {
      console.log(id);
      this.serverId = id;
    },
    setChannel(id) {
      this.channelId = id;
    }
  }
}
</script>
<template>
  <header class="fixed top-0 left-0 h-screen flex flex-row">
    <LeftNav @newServ="setServer">
      <LeftChan :server-id="serverId" :user-id="userId" @setChannel="setChannel">
      </LeftChan>
    </LeftNav>
  </header>
  <Discussion :channel-id="channelId"></Discussion> 
</template>
