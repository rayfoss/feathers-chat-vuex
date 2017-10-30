<template>
  <div>
    <form class="flex flex-row flex-space-between" id="send-message" v-on:submit.prevent>
      <input type="text" name="text" class="flex flex-1" v-model="newMessage">
      <button class="button-primary" type="submit" @click="addMessage">Send</button>
    </form>
    <form class="flex flex-row flex-space-between" id="send-message" v-on:submit.prevent>
      <input type="text" name="text" class="flex flex-1" v-model="oldMessage.text">
      <button class="button-primary" type="submit" @click="reviseMessage">Patch</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'MessageComposer',
  data () {
    return {
      newMessage: '',
      oldMessage: {text: ''}
    }
  },
  props: {
    createMessage: Function,
    patchMessage: Function
  },
  methods: {
    addMessage () {
      // Create a new message and then clear the input field
      this.createMessage({text: this.newMessage}).then(this.clearMessage)
    },
    reviseMessage () {
      // Create a new message and then clear the input field
      debugger
      this.patchMessage(this.oldMessage._id, {text: this.oldMessage.text}, {}).then(this.clearMessage)
    },
    clearMessage (result) {
      this.newMessage = ''
      this.$set(this, 'oldMessage', result)
    }
  }
}
</script>
