<template>
<div class="chat">

    <div class="messageArea" @change="scrollToBottom">
        <p class="message" ref="messages" 
            v-for="chatMessage in this.chatMessages" :key="chatMessage" :class="chatMessage.user">
            {{chatMessage.text}} 
        </p>
    </div>

    <div class="inputArea">
        <input class="inputMessage" type="text" placeholder="Digite sua mensagem" @keypress.enter="sendMessage" v-model="this.message"/>

        <svg class="inputSend" @click="sendMessage" viewBox="0 0 24 24" width="24" height="24" fill="none" 
            stroke-linecap="round" stroke-linejoin="round" stroke="currentColor" stroke-width="2">
            <line x1="22" y1="2" x2="11" y2="13"/>
            <polygon points="22 2 15 22 11 13 2 9 22 2"/>
        </svg>
    </div>
    
</div>
</template>

<script>
export default {
    name: 'ChatComponent',
    data() {
        return {
            message: null,
            chatMessages: [
                {
                    user: "bot",
                    text: "teste bot"
                },
                {
                    user:"user",
                    text: "teste usuário"
                }
            ],
            randomMessages: [
                "Tudo o que um sonho precisa para ser realizado é alguém que acredite que ele possa ser realizado",
                "Devíamos ser ensinados a não esperar por inspiração para começar algo. Ação sempre gera inspiração. Inspiração raramente gera ação",
                "Não importa que você vá devagar, contanto que você não pare",
                "A inspiração existe, porém temos que encontrá-la trabalhando."
            ]
        }
    },
    methods: {
        sendMessage(){
            if(!this.message)
                return;

            let sentMessage = {
                user: "user",
                text: this.message
            };

            this.message = "";

            this.chatMessages.push(sentMessage);

            this.$nextTick(this.scrollToBottom);

            setTimeout(this.sendBotMessage, 1000);
        },

        sendBotMessage() {
            let messageIndex = Math.floor(Math.random() * this.randomMessages.length);

            let sentMessage = {
                user: "bot",
                text: this.randomMessages[messageIndex]
            };

            this.chatMessages.push(sentMessage);

            this.$nextTick(this.scrollToBottom); 
        },
        
        scrollToBottom() {
            let lastMessage = this.$refs.messages.slice(-1)[0];
                        
            lastMessage.scrollIntoView();
        }
    }
}
</script>

<style scoped>
* {
    margin: 0px;

    --bot-background-color: rgb(229, 229, 234);
    --bot-message-color: black;

    --user-background-color:  rgb(36, 139, 245);
    --user-message-color: white;

    --background-chat-color: white;
    --icon-chat-color: black;
}

.chat {
    position: fixed;
    right:20px;
    bottom: 10px;

    display: grid;
    grid-template-rows: 9fr 1fr;
    grid-gap: 10px;

    padding: 10px;
    padding-top: 20px;

    width: 30%;
    max-width: 400px;
    min-width: 300px;

    height: 50%;
    min-height: 200px; 
    max-height: 500px;
    
    background-color: var(--background-chat-color);
    color: var(--font-color);

    box-shadow: 5px 5px 6px 6px grey;
    border-radius: 20px;
}

.inputArea {
    display: inline-grid;
    grid-template-columns: 15fr 1fr;

    align-items: center;
    justify-items: stretch;

    background-color: var(--background-chat-color);

}

.inputMessage {
    padding: 20px;
    border-radius: 20px;
    border: solid 1px;

    background-color: var(--user-message-coloror);
}

.inputSend {
    height: 30px;
    bottom: 10px;
    rotate: 45deg;
    color: var(--icon-chat-color);
} 

.messageArea {
    overflow: auto;
    padding: 10px;

    display: flex;
    flex-direction: column;
    flex-grow: 10;
    gap: 10px;
}

.message {
    width: 75%;
    padding: 15px;

    overflow-wrap: break-word;

    border-radius: 20px;

    color: white;
    font-family: Arial, Helvetica, sans-serif;

    text-align: left;
}

.bot {
    background-color: var(--bot-background-color);
    color: var(--bot-message-color);

    border-bottom-left-radius: 5px;
    box-shadow: 2px -2px var(--shadow-message-color);

    align-self: flex-start;
}

.user {
    background-color: var(--user-background-color);
    color: var(--user-message-color);

    border-bottom-right-radius: 5px;
    box-shadow: -2px -2px var(--shadow-message-color);

    align-self: flex-end;
}

/* Scrollbar */
/* width */
::-webkit-scrollbar {
    width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
    background: #f1f1f1; 
}

/* Handle */
::-webkit-scrollbar-thumb {
    background: #888;
    border-radius: 10px;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
    background: #555; 
}

</style>
