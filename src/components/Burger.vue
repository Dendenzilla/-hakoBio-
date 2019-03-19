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
