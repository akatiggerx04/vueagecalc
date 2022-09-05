<script lang="ts">

var emoji = {
    "newborn": "👶",
    "young": "🧒",
    "teen": "🧒",
    "adult": "🧑",
    "old": "🧓",
    "veryold": "💀",
    "alien": "🛸"
};

import { defineComponent } from 'vue'

export default defineComponent({
  data() {
    return {
      message: '',
      emj: ''
    }
  },
  methods: {
    onInput(e) {
        if (e.target.value == null || e.target.value == '') {
            this.message = '';
            this.emj = '';
            return;
        }
        let bornyear = Number(e.target.value);
        let currentyear = new Date().getFullYear();
        if (bornyear > currentyear) {
            this.emj = emoji["alien"];
            if (bornyear == 2077) {
                this.message = `あなたはタイムトラベラーですか??`;
            } else {
                this.message = `Are you a time traveler 🤨??`;
            }
            return;
        }
        let age = currentyear - bornyear;
        if (age < 2) {
            this.message = `You are a new born :D`;
            this.emj = emoji["newborn"];
            return;
        }
        if (age < 3) {
            this.emj = emoji["newborn"];
        } else if (age < 10) {
            this.emj = emoji["young"];
        } else if (age < 16) {
            this.emj = emoji["teen"];
        } else if (age < 45) {
            this.emj = emoji["adult"];
        } else if (age < 120) {
            this.emj = emoji["old"];
        } else {
            this.emj = emoji["veryold"];
        }
        if (age > 250) {
            this.message = `You are ${age} years old :O`;
        } else {
            this.message = `You are ${age} years old!`;
        }
    }
  }
})
</script>
<template>
    <div>
        <h1 class="title">What Year Were You Born In?</h1><br>
        <input type="number" @input="onInput" placeholder="Example: 1998">
        <p class="emoji">{{ emj }}</p>
        <p class="agetext">{{ message }}</p>
        <footer>Built with ❤️ by akatiggerx04.</footer>
    </div>
</template>