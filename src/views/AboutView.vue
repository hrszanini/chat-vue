<template>
<div class="about">
    <h1>This is an about page</h1>
    <chat-component/>
</div>
</template>

<script>
import ChatComponent from '@/components/ChatComponent.vue'

export default {
    name: 'HomeView',
    components: {
        ChatComponent
    }
}
</script>
