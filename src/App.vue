<template>
  <div id="app" class="app">
    <div class="app__inner">
    <img alt="picture" src="./assets/component.png" class="app__picture">
    <div class="app__title">
      <h2 class="title-text">Beautiful landscape</h2>
      <button class="btn btn-donate" :disabled='true'>Donate Author</button>
    </div>
   
    <comment-list></comment-list>
    </div>
    
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import CommentList from './components/CommentList'

export default {
  name: 'app',
  components: {
    HelloWorld,
    CommentList
  },
  data() {
    return {
    
    }
   
 
  },
   methods: {

    }
 
}
</script>

<style lang="scss">
@mixin placeholder {
  &::-webkit-input-placeholder {
    @content;
  }
  &:-moz-placeholder {
    @content;
  }
  &::-moz-placeholder {
    @content;
  }
  &:-ms-input-placeholder {
    @content;
  }
}

.app {
    box-sizing: border-box;
font-family: 'Montserrat', sans-serif;
height: 100vh;
background-color: #F0F0F0;
display: flex;
justify-content: center;
align-items: center;
 &__inner {
   box-sizing: border-box;
   width: 568px;
   background-color: #fff;
   border-radius: 8px;
   padding: 16px;
 }
 &__picture {
   max-width: 100%;
 }
 &__title {
   display: flex;
   justify-content: space-between;
   padding-top: 16px;
   padding-bottom: 16px;
   .title {
     &-text {
       margin: 0;
       font-weight:400;
       font-size: 20px;
       line-height: 24px;
     }
   }
 }
}
.btn {
  &-donate {
    background: linear-gradient(to right, #bec2f3 0%, #f7caeb 160%);
    padding: 8px 16px;
    border-radius: 4px;
    border:0;
    cursor: pointer;
    font-weight: 600;
    font-size: 11px;
    line-height: 14px;
  
  }
  &-send {
    display: block;
    cursor: pointer;
    font-size: 11px;
    color:#fff;
    border-radius: 4px;
    background-color: #2C3BFF;
    border: 1px solid #2C3BFF;
    padding: 0px;
      width: 88px;
      transition: 0.3s;
   &.hidden {
   width: 0px;
   padding: 0;
   border: 0;
   font-size:0;
  }
  }
}
.comments {
  &-field {
 display: flex;
 justify-content: space-between;
 width: 100%;
  }
  &-input {
    display: block;
    width: 100%;
  height: 46px;
  padding-left: 16px;
      border-radius: 4px;
      border: 0.5px solid #707070;
      padding-top: 0;
      padding-bottom: 0;
      box-sizing: border-box;
    @include placeholder {    
font-weight: 400;
font-size: 16px;
color:#666666;
line-height: 19px;
    }
&:focus {
  border-color:#2C3BFF;
}
  }
}



</style>



