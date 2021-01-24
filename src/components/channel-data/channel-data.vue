<template>
<div class="container">
    <div class="messages">
        <!-- Messages Componenets -->
        <!-- <ChannelMessage
        v-for="message in 1"
        :key="message"
        authorName="TMCHVD"
        :date="getDate"
      >
        Chào mừng tới buổi giải đáp Q&A của TMCHVD
      </ChannelMessage> -->
        <div v-for="qna in qnas" :key="qna.id">
            <ChannelMessage isBot hasMention authorName="User" :date="getDate">
                <Mention>TMCHVD</Mention> {{ qna.question }}
            </ChannelMessage>

            <ChannelMessage isHarry v-if="qna.harry.length" authorName="Harry" :date="getDate">
                {{ qna.harry }}
            </ChannelMessage>
            <ChannelMessage isOkakoro v-if="qna.okakoro.length" authorName="OkaKoro" :date="getDate">
                {{ qna.okakoro }}
            </ChannelMessage>
            <ChannelMessage isInu v-if="qna.inu.length" authorName="Hwang Inu" :date="getDate">
                {{ qna.inu }}
            </ChannelMessage>
            <ChannelMessage isToki v-if="qna.toki.length" authorName="Toki" :date="getDate">
                {{ qna.toki }}
            </ChannelMessage>
            <ChannelMessage isHaru v-if="qna.haru.length" authorName="Haruki" :date="getDate">
                {{ qna.haru }}
            </ChannelMessage>
            <ChannelMessage isOi v-if="qna.oi.length" authorName="Oi" :date="getDate">
                {{ qna.oi }}
            </ChannelMessage>
            <ChannelMessage isKuro v-if="qna.kuro.length" authorName="Kuro" :date="getDate">
                {{ qna.kuro }}
            </ChannelMessage>
            <ChannelMessage isGin v-if="qna.gin.length" authorName="Gin" :date="getDate">
                {{ qna.gin }}
            </ChannelMessage>
            <ChannelMessage isTmchvd v-if="qna.tmchvd.length" authorName="TMCHVD" :date="getDate">
                {{ qna.tmchvd }}
            </ChannelMessage>
        </div>
    </div>
    <div class="input-wrapper">
        <input type="text" name="message" v-model="message" placeholder="Type a message here, and press enter." id="input-message" @keypress.enter="writeMessage(message)" />
        <div class="icon">
            <At :size="24" />
        </div>
    </div>
</div>
</template>

<script>
import At from 'vue-material-design-icons/At'
import {
    io
} from 'socket.io-client'
// Compoenents
import ChannelMessage from './channel-message'
import Mention from './mention'
import qna20210115 from './qna20210115'

export default {
    components: {
        At,
        ChannelMessage,
        Mention,
    },
    data() {
        return {
            messagesArray: [],
            message: '',
            date: '',
            qnas: qna20210115,
        }
    },
    // Get initial messages from the server (enable the "created()" function to connect with the server)
    /* created() {
      this.socket = io('http://localhost:3001/')
      this.socket.on('getInitialMessages', (messages) => {
        this.messagesArray = messages
      })
    }, */
    // Sending messages to server, and getting the returned messages
    methods: {
        writeMessage(message) {
            this.socket.emit('sendMessage', message)
            this.message = ''
            this.getReturnedMessage()
        },
        getReturnedMessage() {
            this.socket.on('returnMessage', (messages) => {
                this.messagesArray = messages
            })
        },
    },
    // Get date
    computed: {
        getDate() {
            return new Date().toString()
        },
    },
}
</script>

<style lang="scss" scoped>
.container {
    grid-area: cd;
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    flex-flow: column nowrap;
    background-color: var(--primary);
    flex: 1;
}

.input-wrapper {
    width: 100%;
    padding: 0 16px;
    height: 68px;

    input {
        margin-top: 12px;
        width: 100%;
        height: 44px;
        padding: 0 10px 0 57px;
        border-radius: 5px;
        color: var(--white);
        background-color: var(--chat-input);

        &::placeholder {
            color: var(--grey);
            font-size: 16px;
        }
    }

    .icon {
        color: var(--grey);
        position: relative;
        top: -50%;
        left: 14px;
        transition: 0.2s;
        width: 24px;
    }
}

.messages {
    display: flex;
    flex-direction: column;
    height: calc(100vh - 46px - 68px);
    max-height: calc(100vh - 46px - 68px);
    overflow-y: scroll;

    .channelmessage:first-child {
        margin-top: 0;
    }

    &::-webkit-scrollbar {
        width: 8px;
    }

    &::-webkit-scrollbar-thumb {
        background-color: var(--tertiary);
        border-radius: 4px;
    }

    &::-webkit-scrollbar-track {
        background-color: var(--primary);
    }
}

.link {
    color: var(--grey);
    outline: none;
}
</style>
