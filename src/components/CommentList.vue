<template>
    <div class="comments">
         <div class="comments-field">
      <input type="text" class="comments-input" placeholder="Write a new comment" @focus="showBtn" @blur='hideBtn' v-model='message'>
      <button class="btn btn-send" :class="[isVisible ? '' : 'hidden']" @click='addComments'>Send</button>
    </div>
             <comment
              v-for="(item, index) in commentsList"
              :comments='item'
              :key = 'index'
              v-on:delete-comment = 'deleteComment'
             
             ></comment>    
    </div>
</template>

<script>
import Comment from './Comment'

export default {
  name: 'CommentsList',
  components: {
      Comment
  },

data(){
    return {
     isVisible:false,
   
     message:'',
    commentsList:[ 
         {  name:'Jason X', text: "That's awesome! What techniques are you used to took it?" },
         {  name:'Land Warrior 17', text: "I've been there, that was nice meeting on battleground!" },
         {  name:'WWII', text: "That's awesome!" },
    ],
    }
},
 methods: {
    showBtn(e) {
      this.isVisible = true;     
    },
    hideBtn() {
      
    },
    addComments(){
        if(this.message.length >0) {
        this.commentsList.unshift({name:'Egor',text:this.message})
      this.isVisible = false;
      this.message='';
        }
    },
    deleteComment(comments) {
        const commentsListIndex = this.commentsList.indexOf(comments);
        this.commentsList.splice(commentsListIndex, 1);
         
    },

  }
 
}
</script>

<style lang="scss" scoped>

</style>


