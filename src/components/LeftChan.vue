<script setup>
defineProps({
    serverId: Number,
    userId: Number
});
</script>
<script>
export default {
    emits: ['setChannel'],
    data() {
        return {
            currentChan:1,
            chevron: true,
            mic: true,
            sound: true
        }
    },
    methods: {
        setChannel(channelId){
            this.currentChan = channelId;
            this.$emit('setChannel', channelId);
        }
    },
    computed: {
        server() {
            return window.getServer(this.serverId);
        },
        user() {
            return window.getUser(this.userId);
        },
        channels() {
            return window.getChannels();
        }
    }

}
</script>
<template>
    <nav class="flex flex-col w-60 m-0 bg-zinc-800 h-screen text-white relative">
        <h1 class="p-4 font-bold text-lg shadow-sm shadow-black">{{ server.name }}</h1>
        <div class="flex flex-col">
            <div
                class="p-1 px-2 m-2 mb-0 text-gray-400 uppercase font-semibold"
                v-for="cat in server.cats"
            >
                <h2 class="hover:text-white">
                    <i
                        class="text-xs fa fa-chevron-down cursor-pointer"
                        :class="{ 'fa-chevron-down': cat.chevron, 'fa-chevron-right': !cat.chevron }"
                        @click="cat.chevron = !cat.chevron"
                    ></i>
                    {{ cat.name }}
                </h2>
                <ul class="duration-300 ease-linear origin-top" :class="{ 'hidden': !cat.chevron }">
                    <li
                        v-for="chan in cat.chans"
                        class="normal-case p-1 px-2 cursor-pointer hover:text-white hover:bg-zinc-600 rounded-sm"
                        @click="setChannel(chan)"
                        :class="{'text-white bg-zinc-700':(currentChan === chan )}"
                    >
                        <i class="fas fa-hashtag"></i>&nbsp;
                        <span>{{ channels[chan]?.name }}</span>
                    </li>
                </ul>
            </div>
            {{ server }}
        </div>
        <div class="flex flex-col-reverse fixed bottom-0 w-60">
            <div class="flex px-2 border-t-gray-500 border-t">
                <figure>
                    <img
                        class="relative flex items-center justify-center h-10 w-10 mt-2 mb-2 mx-auto shadow-lg rounded-3xl cursor-pointer"
                        src="../assets/rosie-avatar.png"
                        alt="{{user.name}}#{{ user.id }}"
                    />
                </figure>
                <div class="font-bold p-2 leading-4 text-sm">
                    {{ user.name }}
                    <br />
                    <span class="font-light">#{{ user.id }}</span>
                </div>
                <div
                    class="flex flex-auto flex-row-reverse items-center justify-right ml-auto mr-0 right-0 p-2"
                >
                    <i class="p-2 fa fa-cog"></i>
                    <i
                        class="p-2 fa fa-headphones-alt"
                        :class="{ 'fa-headphones-alt': sound, 'fa-headphones-alt': !sound }"
                    ></i>
                    <i
                        class="p-2 fa"
                        :class="{ 'fa-microphone': mic, 'fa-microphone-slash': !mic }"
                        @click="mic = !mic"
                    ></i>
                </div>
            </div>
        </div>
    </nav>
</template>
