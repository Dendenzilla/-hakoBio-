<template>
  <div class="chatbot">
    <div class="hako_title">
      <p>HAKO</p>
    </div>
    <div class="robotHead">
      <img v-if="sleeping" class="gif" src="../assets/hako-sleep.gif" alt="">
      <img v-if="thinking" class="gif" src="../assets/hako-loading.gif" alt="">
      <img v-if="unhappy" class="gif" src="../assets/hako-unhappy.png" alt="">
      <img src="../assets/hako-happy.png" alt="">
    </div>
    <div class="chat" id="truc">
      <div v-for="(c,index) in chatlog" :key="index" class="tdiv" v-show="c.text">
          <div v-if="c.type === 'R'" >
            <div class="bubble bot">
              <p>{{c.text}}</p>
              <!-- <img :src="c.text" alt="img"> -->
            </div>
          </div>
          <!--  -->
          <div v-else-if="c.type === 'I'" >
            <div class="bubble bot">
              <img :src="c.text" alt="img"> 
            </div>
          </div>
          <!--  -->
          <div v-else class="tdiv">
            <div class="bubble user">
              <p>{{c.text}}</p>
            </div>
          </div>
          
      </div>
    </div>
    <div class="mouth">
      <form>
        <textarea rows="3" v-model="question" v-on:keyup.enter="post()" placeholder="Type your question here"></textarea>
        <button @click.prevent="post()" >Ask <br>Hako</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { setTimeout } from 'timers';

export default {
    data() {
        return {
          chatlog: [{
            text:`Hi I'm Hako !`,
            type:'R'
          }, {
            text:'Can I help you ?',
            type:'R'
          }
          ],
          question: '',
          sleeping:true,
          thinking: false,
          unhappy: false,
        }
    },
    name:'Chatbot',
    methods: {
        post() {
          this.sleeping = false;
          if (this.question.length > 1) {
            let userQ = this.question;
            this.question = '';
            this.chatlog.push({text:userQ.trim(), type:'Q'});
          
            this.sleeping = false;
            this.unhappy = false;
            this.thinking = true;
            this.$nextTick(() => {
                      this.scrollToEnd();
                    })
            axios.get("https://apihakobot.azurewebsites.net/api/values?question="+userQ).then(response => {
                let botAnswer = response.data;
                if (response.data[0] === "I'm sorry but i can't answer your question. But i'm working on it ! Try again later.") {
                  this.unhappy = true;
                  this.sleeping = false;
                  botAnswer.forEach((a) => {
                    this.chatlog.push({text:a, type:'R'})  
                  })
                  this.$nextTick(() => {
                      this.scrollToEnd();
                    })
                } else {
                setTimeout(() => {
                  this.thinking = false;
                  botAnswer.forEach((a) => {
                    if(/(http(s?):)([/|.|\w|%|-])*/i.test(a)){
                      this.chatlog.push({text:a, type:'I'})
                    }else{
                      this.chatlog.push({text:a, type:'R'})
                    }
                  })
                  
                  this.$nextTick(() => {
                      this.scrollToEnd();
                    })
                  
              }, 1200)}
            })
            } else {
            this.unhappy = true;
            this.question = '';
            this.chatlog.push({text:"You have not submitted a question, please do so.", type:'R'});
            this.$nextTick(() => {
                      this.scrollToEnd();
                    })
            return;
          }
          //Sleep
          setTimeout(() => {
                  this.sleeping = false;
                  this.$nextTick(() => {
                    this.unhappy = false;
                    this.thinking = false;
                    this.sleeping = true;
                    })
              }, 10000)
        // FIN FONCTION POST
        },
        scrollToEnd: function() {
          var container = this.$el.querySelector('#truc');
          container.scrollTop = container.scrollHeight;
        }
    }
}


</script>

<style lang="scss">
.chatbot {
  position: relative;
  height: 450px;
  width: 300px;
  margin: 0 auto;
  border-radius: 6px 6px 0 0;
  background-color: #d3d7d8;
}
.tdiv {
  display: flex;
  flex-direction: column;
  align-items: baseline;
  width: 100%;
}
.robotHead {
  position: absolute;
  top: -35px;
  left: 16px;
  height: 60px;
  width: 65px;
  & img {
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1;
  }
  .gif{
    z-index: 2;
  }
}

.hako_title {
  margin: 0 auto;
  padding: 10px;
  width: 200px;
  text-align: center;
  font-size: 13px;
  font-weight: bold;
  & p {
    margin: 0;
  }
}
.chat {
  overflow-y: auto;
  height: 325px;
  padding: 5px 12px 0 12px;
  width: 276px;
  border-top: 2px solid rgb(208, 210, 211);
  background-color: #e0e6e8;
}
.bot {
  background-color: #00b3b3;
  color: white;
  align-self: flex-start;
  text-align: left;
}
.user {
  background-color: #ff8047;
  color: white;
  text-align: right;
  align-self: flex-end;
}
.bubble {
  padding: 4px 10px;
  border-radius: 8px;
  margin-top: 2px;
  margin-bottom: 8px;
  max-width: 80%;
  overflow-wrap: break-word;
  max-width: 210px;
  & img {
    width: 100%;
  }
}
.chat p {
  margin: 0;
}
form{
  display: flex;
  justify-content: center;
}
textarea {
  width: 70%;
  resize: none;
  font-family: Montserrat;
  border-color:transparent;
  border-radius: 8px 0 0 8px;
  padding:5px;
  font-size: 14px;
}

textarea:focus{
  outline-color: #00b3b3;
}

button{
  color: #fff;
  background:#0b1927;
  border-radius: 0 8px 8px 0;
  border: 1px solid #0b1927;
  cursor: pointer;
}
button:hover{
  border:1px solid #00b3b3;
  background-color:#00b3b3;
}

.mouth {
  position:fixed;
  top: 423px;
  width: 300px;
  border-top: 2px solid rgb(208, 210, 211);
  padding: 12px 0;
  background-color: #e0e6e8;
}

.hidden{
  display: none;
}
</style>
