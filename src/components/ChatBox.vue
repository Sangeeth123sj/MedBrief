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
    <br/><br/>
    <strong class="answer-align">{{this.answer}}</strong>
  </div>
  <div class="input-area">
    
    <form @submit.prevent="submitForm">
       
    <input type="text" v-model="question" class="input-field" placeholder="chat">
   
    <button class="btn btn-primary chat-button">Send
      <div v-if="loadingAnswer" >
            <i class="fa fa-spinner fa-spin"></i>
          </div>
    </button>
    </form>
  </div>
</div>
</template>

<script>
import Cookies from "js-cookie";
export default {
  data() {
    return {
      messages: [],
      newMessage: "",
      report: null,
      question:null,
      reportStatus:false,
      answer:null,
      loadingAnswer:false
    };
  },
  methods: {
    submitForm(){
      this.report = Cookies.get("report");
      if (this.report){
        this.loadingAnswer = true;
        this.reportStatus = true
         try {
          fetch(
            
            // "http://127.0.0.1:8000/q_and_a/" 
            "https://medbriefbackend-production.up.railway.app/q_and_a/"+ this.report+`\nQuestion:`+this.question,
            // {
            //   headers: {
            //     Accept: "application/json",
            //     Authorization: `Bearer ${this.accessToken}`,
            //   },
            // }
          )
            .then((response) => {
              return response.json();
            })
            .then((data) => {
              console.log(data["answer"]);
              
             
              this.answer = data["answer"];
              this.loadingAnswer = false;

              
            });
        } catch (error) {
          console.log(error);
          this.answer = "Something went wrong please try again."
          this.loadingAnswer = false;
        }


      }
      else{
          this.answer = "Please submit and summarize the report first."
          console.log(Cookies.get("report"))
      }
    },
    sendMessage() {
      this.messages.push({
        text: this.newMessage,
        sent: true
      });
      this.newMessage = "";
    }
  },
  mounted(){
    Cookies.remove("report");
    
  },
};
</script>
  
  <style>

.rectangle {
  width: 100%;
  height: 90%;
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
.answer-align{
  float: left;
  padding: 10px;
}
</style>
