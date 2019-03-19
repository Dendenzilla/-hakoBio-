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
                <form action="">
                    <textarea rows="3" placeholder="Type your question here"></textarea>
                </form>
            </div>
    </div>
</template>

<script>
export default {
name:'Chatbot'
}
</script>

<style lang="scss">
.chatbot{
    position: relative;
    height: 450px;
    width: 300px;
    margin: 0 auto;
    border-radius: 6px 6px 0 0;
    background-color: #E0E6E8;
    padding-top: 30px;
}
.robotHead {
    position: absolute;
    top: -20px;
    left:20px;
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
    background-color: #00B3B3;
    color: white;
    align-self: flex-start;
    text-align: left;
}
.user {
    background-color: #FF8047;
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
    background-color:#E0E6E8;
}
</style>
