<template>
  <div class="chatbot">
    <div class="hako_title">
      <p> HAKO</p>
    </div>
    <div class="robotHead">
      <img src="../assets/hako-happy.png">
    </div>
    <div class="chat">
      <div v-for="(c,index) in chatlog" :key="index" class="tdiv" v-show="c.text">
          <div v-if="c.type === 'R'" >
            <div class="bubble bot">
              <p>{{c.text}}</p>
            </div>
          </div>
          <div v-else class="tdiv">
            <div class="bubble user">
              <p>{{c.text}}</p>
            </div>
          </div>
      </div>
    </div>
    <div class="mouth">
      <form action>
        <textarea rows="3" v-model="question" placeholder="Type your question here"></textarea>
        <button @click.prevent="post()">Ask <br>Hako</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
    data() {
        return {
          chatlog: [{
            text:`Hi I'm Hako ! Can I help you ?'`,
            type:'R'
          }
          ],
          question: ''
        }
    },
    name:'Chatbot',
    methods: {
        post() { 
          this.chatlog.push({text:this.question, type:'Q'});
            var headers = {
                'Content-Type': 'application/json',
                'Authorization': 'EndpointKey afdff838-d95c-40d3-a32d-b0488a1ee7e5' 
            }
            axios.post("https://qnabxl.azurewebsites.net/qnamaker/knowledgebases/09ae110d-19ea-407c-bbea-0c4cdf8383f3/generateAnswer", {"question":this.question} ,{headers: headers} ).then(response => {
                let botAnswer = response.data;
                this.question = '';
                this.chatlog.push({text:botAnswer.answers[0].answer, type:'R'});
            })
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
  }
}
.hako_title {
  margin: 0 auto;
  padding: 10px;
  width: 200px;
  text-align: center;
  font-size: 13px;
  & p {
    margin: 0;
  }
}
.chat {
  overflow-y: scroll;
  height: 325px;
  padding: 0 12px;
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
  margin-bottom: 8px;
  max-width: 80%;
  overflow-wrap: break-word;
  max-width: 210px;
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
  border-radius: 15px 0 0 15px;
  padding:5px;
  // box-shadow: 3px 5px 15px #e0e6e8 inset;
}

textarea:focus{
  outline-color: #00b3b3;
}

button{
  color: #fff;
  background:#0b1927;
  border-radius: 0 15px 15px 0;
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
</style>
