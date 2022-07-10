<template>
  <div class="background" @click.self="accepted()">
    <div class="main">
        <ol>
            <li>
                Lorem Ipsum is simply dummy text of the printing and typesetting industry.
                Lorem Ipsum has been the industry's standard dummy text ever since the 1500s,
                when an unknown printer took a galley of type and scrambled it to make a type specimen book.
                It has survived not only five centuries, but also the leap into el
            </li>
            <br>
            <li>
                Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut 
                labore et dolore magna aliqua. Ut enim ad minim veniam,
                quis nostrud exercitation ullamco laboris nisi ut
            </li>
            <br>
            <li>
                Aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
            </li>
        </ol>
        <button @click="accepted()" class="closeBut">Close</button>
    </div>
  </div>
</template>

<script>
export default {
    name:'PrivacyVue',
    methods:{
        accepted(){
            this.$emit('ruleAccepted');
        }
    }
}
</script>

<style>
.background{
    background-color: rgba(0, 0, 0, 0.7);
    position: fixed;
    height: 972px;
}
.main{
    background-color: white;
    border-radius: 15px;
    text-align: left;
    height: 400px;
    width: 50%;
    margin: 0 auto;
    margin-top: 150px;
    padding: 30px;
    position: relative;
    font-weight: 501;
    text-align: justify;
}
.closeBut{
    background-color: red;
    color: white;
    padding: 10px 15px;
    border: 0px;
    font-weight: 600;
    letter-spacing: 1px;
    font-size: 12px;
    border-radius: 10px;
    margin: 0 auto;
    display: block;
    margin-top: 25px;
    cursor: pointer;
}
</style>