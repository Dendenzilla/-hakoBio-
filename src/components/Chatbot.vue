<template>
  <div class="chatbot">
    <div class="hako_title">
      <p>Hako</p>
      <p>T</p>
    </div>
    <div class="robotHead">
      <img src="../assets/hako-happy.png">
    </div>
    <div class="chat">
      <div class="bubble bot">
        <p>OKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKK</p>
      </div>
      <div class="bubble user">
        <p>Lorem ipsum dolor sit</p>
      </div>
      <div class="bubble user">
        <p>Lorem ipsum dolor sit</p>
      </div>
      <div class="bubble user">
        <p>Lorem ipsum dolor sit</p>
      </div>
      <div class="bubble bot">
        <p>Une phrase corecte pour voir si ça se met nbien</p>
      </div>
      <div class="bubble user">
        <p>Lorem ipsum dolor sit</p>
      </div>
      <div class="bubble user">
        <p>Lorem ipsum dolor sit</p>
      </div>
      <div class="bubble user">
        <p>Lorem ipsum dolor sit</p>
      </div>
      <div class="bubble user">
        <p>Lorem ipsum dolor sit</p>
      </div>
      <div class="bubble user">
        <p>Lorem ipsum dolor sit</p>
      </div>
    </div>
    <div class="mouth">
      <form action>
        <textarea rows="3" v-model="userQ" placeholder="Type your question here"></textarea>
        <button @click.prevent="post()">Ask Hako</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

/*export default {
    data() {
        return {
            userQ: 'hakobio',
            questions: []
        }
    },
    name:'Chatbot',
    methods: {
        post() {
            console.log('test')
            var headers = {
                'Content-Type': 'application/json',
                'Authorization': 'EndpointKey afdff838-d95c-40d3-a32d-b0488a1ee7e5' 
            }
            axios.post("https://qnabxl.azurewebsites.net/qnamaker/knowledgebases/09ae110d-19ea-407c-bbea-0c4cdf8383f3/generateAnswer", {"questions":"hakobio"} ,{headers: headers} ).then(response => {
                this.questions = response.data;
                console.log('test2')
            })
        }
    }
}*/

export default {
    data() {
        return {
            userQ: '',
            questions: ''
        }
    },
    name:'Chatbot',
    created() {
        var headers = {
            'Content-Type': 'application/json',
            'Authorization': 'EndpointKey afdff838-d95c-40d3-a32d-b0488a1ee7e5' 
        }
        axios.post("https://qnabxl.azurewebsites.net/qnamaker/knowledgebases/09ae110d-19ea-407c-bbea-0c4cdf8383f3/generateAnswer",{"question":"What is hakobio"} ,{headers: headers} ).then(response => {
            this.questions = response.data;
        })
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
.robotHead {
  position: absolute;
  top: -35px;
  left: 6px;
  height: 60px;
  width: 60px;
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
  max-height: 400px;
  display: flex;
  flex-direction: column;
  align-items: baseline;
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
textarea {
  width: 90%;
  resize: none;
  font-family: Montserrat;
}
.mouth {
  bottom: 12px;
  width: 100%;
  border-top: 2px solid rgb(208, 210, 211);
  padding: 12px 0;
  background-color: #e0e6e8;
}
</style>
