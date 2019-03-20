<template>
    <div>
        <h1>lay burgeurs</h1>
        <div v-for="(b, index) in burgers" :key="index">
            <h2>{{b.quantity ? b.quantity : "&nbsp;"}} {{b.name}}<span v-if="b.veggie">🌿</span></h2>
        </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
    name:'Burger',
    data() {
        return {
        burgers: []
        }
    },
    created() {
    axios.get("https://wt-902485dbb4fca4fccee3a0efcde5b34c-0.sandbox.auth0-extend.com/orderfoodmenu")
      .then(response => {
        this.burgers = response.data;
      })
    }
}
</script>

<style>

</style>


methods: {
        post() {
            this.chatlog.push({text:this.question.trim(), type:'Q'});
            this.loading = true;
            console.log(this.loading)
            this.$nextTick(() => {
                      this.scrollToEnd();
                    })
            var headers = {
                'Content-Type': 'application/json',
                'Authorization': 'EndpointKey afdff838-d95c-40d3-a32d-b0488a1ee7e5' 
            }
            axios.post("https://qnabxl.azurewebsites.net/qnamaker/knowledgebases/09ae110d-19ea-407c-bbea-0c4cdf8383f3/generateAnswer", {"question":this.question} ,{headers: headers} ).then(response => {
                let botAnswer = response.data;
                  if (this.question.length > 1) {
                  this.question = '';
                  this.chatlog.push({text:botAnswer.answers[0].answer, type:'R'});
                  } else {
                    this.question = '';
                    this.chatlog.push({text:'How about you actually submit a question, genius.', type:'R'});
                    
                    
                  }
                  this.$nextTick(() => {
                      this.scrollToEnd();
                    })
            })
            this.loading = false
        },
        scrollToEnd: function() {
          var container = this.$el.querySelector('#truc');
          container.scrollTop = container.scrollHeight;
        }
    }