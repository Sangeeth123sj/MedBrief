<template>

  <!-- <div class="chat">
    <div class="chat-box">
      <div class="message-container" v-for="message in messages">
        <div class="message" :class="{ 'message-sent': message.sent }">
          {{ message.text }}
        </div>
      </div>
      <div class="message-form">
        <textarea v-model="newMessage" @keyup.enter="sendMessage" rows=20></textarea>
        <br/><br/>
        <button @click="sendMessage" class="btn btn-primary">Send</button>
      </div>
    </div>
  </div> -->
  <h2>Q & A</h2>
<div class="rectangle">
  <div class="message-area">
    
  </div>
  <div class="input-area">
    <input type="text" class="input-field" placeholder="chat">
    <br/><br/>
    <button class="send-btn">Send</button>
  </div>
</div>
</template>

<script>
export default {
  data() {
    return {
      messages: [],
      newMessage: ""
    };
  },
  methods: {
    sendMessage() {
      this.messages.push({
        text: this.newMessage,
        sent: true
      });
      this.newMessage = "";
    }
  }
};
</script>
  
  <style>

.rectangle {
  width: 100%;
  height: 80%;
  border: 1px solid black;
  position: relative;
  border-radius:5px;
}

.message-area {
  width: 100%;
  height: 80%;
  overflow: scroll;
}

.input-area {
  
  position: absolute;
  bottom: 0;
  width: 100%;
  display: flex;
  align-items: center;
  padding: 10px;
}

.input-field {
  flex-grow: 1;
  padding: 10px;
  border: 2px;
  border-color: black;
  border-radius: 10px;
  margin-right: 10px;
  outline: 3px solid black;
}

.send-btn {
  background-color: blue;
  color: white;
  
  border: none;
  border-radius: 10px;
  cursor: pointer;
  

}

.chatbox-input button {
  padding: 5px 10px;
  border-radius: 5px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}
textarea {
width: 100%; /* or any desired width in pixels or percentage */
}
</style>
