<template>
  <div class="sc-message" style="display:flex;justify-content:center;flex-direction:column;">
    <div class="sc-message--content" :class="{sent: message.author === 'me', received: message.author !== 'me'}">
      <!--<div class="sc-message--avatar" :style="{ backgroundImage: `url(${this.chatIcon})` }"></div>-->
      <TextMessage v-if="message.type === 'text'" :data="message.data" />
      <EmojiMessage v-else-if="message.type === 'emoji'" :data="message.data" />
      <FileMessage v-else-if="message.type === 'file'" :data="message.data" />
    </div>
    <template v-if="message.datetime">
    <div :style="'margin-top:5px;font-size:12px;color:#999999;text-align:'+ (message.author === 'me' ? 'right;' : 'left;')">
        {{message.datetime}}
    </div>
    </template>
  </div>
</template>

<script>
import TextMessage from './TextMessage.vue'
import FileMessage from './FileMessage.vue'
import chatIcon from './assets/chat-icon.svg'

export default {
  data () {
    return {
      chatIcon
    }
  },
  components: {
    TextMessage,
    FileMessage
  },
  props: {
    message: {
      type: Object,
      required: true
    }
  }
}
</script>
<style>
.sc-message {
  width: 300px;
  margin: auto;
  padding-bottom: 10px;
  display: flex;
}

.sc-message--content {
  width: 100%;
  display: flex;
}

.sc-message--content.sent {
  justify-content: flex-end;
}

.sc-message--content.sent .sc-message--avatar {
  display: none;
}

.sc-message--avatar {
  background-image: url(https://d13yacurqjgara.cloudfront.net/assets/avatar-default-aa2eab7684294781f93bc99ad394a0eb3249c5768c21390163c9f55ea8ef83a4.gif);
  background-repeat: no-repeat;
  background-size: 100%;
  background-position: center;
  min-width: 30px;
  min-height: 30px;
  border-radius: 50%;
  align-self: center;
  margin-right: 15px;
}

.sc-message--meta {
  font-size: xx-small;
  margin-bottom: -10px;
  color: white;
  text-align: center;
}

@media (max-width: 450px) {
  .sc-message {
    width: 80%;
  }
}

.sc-message--text {
  padding: 17px 20px;
  border-radius: 6px;
  font-weight: 300;
  font-size: 14px;
  line-height: 1.4;
  white-space: pre-wrap;
  -webkit-font-smoothing: subpixel-antialiased
}
.sc-message--content.sent .sc-message--text {
  color: white;
  background-color: #4e8cff;
  max-width: calc(100% - 120px);
  word-wrap: break-word;
}

.sc-message--content.received .sc-message--text {
  color: #263238;
  background-color: #f4f7f9;
  margin-right: 40px;
}
</style>
