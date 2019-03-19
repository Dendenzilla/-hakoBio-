<template>
  <div class="chatbot">
    <div class="robotHead"></div>
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
        <button @click.prevent="post()">TEXTE</button>
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
            userQ: 'hakobio',
            questions: ''
        }
    },
    name:'Chatbot',
    created() {
        console.log('test')
        var headers = {
            'Content-Type': 'application/json',
            'Authorization': 'EndpointKey afdff838-d95c-40d3-a32d-b0488a1ee7e5' 
        }
        axios.post("https://qnabxl.azurewebsites.net/qnamaker/knowledgebases/09ae110d-19ea-407c-bbea-0c4cdf8383f3/generateAnswer",{"question":"What is hakobio"} ,{headers: headers} ).then(response => {
            this.questions = response.data;
            console.log('test2')
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
  background-color: #e0e6e8;
  padding-top: 30px;
}
.robotHead {
  position: absolute;
  top: -20px;
  left: 20px;
  height: 40px;
  width: 40px;
  background-color: blue;
}
.chat {
  overflow-y: scroll;
  max-height: 400px;
  display: flex;
  flex-direction: column;
  align-items: baseline;
  padding: 0 12px;
  width: 276px;
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
