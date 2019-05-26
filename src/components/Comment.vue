<template>
<div class="comments-item " >
   <template v-if='isShow'>  
       <div class="item-avatar" >
                <img src="../assets/av-1.png" alt="">         
            </div>
             <div class='item-action' :class="[isVisible ? '' : 'hidden']" >
                 <span class="edit" @click="editMessage">Edit</span>
                 <span class="delete" @click="showDelete">Delete</span>
             </div>
         <div class="item-info"  @click='showAction'>          
                <div class="item-info_name">
                   {{comments.name}}
                </div>
                <div class="item-info_text">
                    {{comments.text}}
                </div>

            </div></template> 

           <div class="delete-field" v-show='isDelete'>
               <span>Delete message?</span>
               <button @click='hideDelete'>No</button>
               <button @click="deleteComment(comments)">Yes</button>
           </div>
                  <div class="comments-field" v-show='isEditing' >
              <input type="text" class="comments-input" placeholder="Write a new comment"  v-model.lazy='comments.text' @blur='hideEditComment(comments)' >
              <button class="btn btn-send" :class="[isVisible ? '' : 'hidden']" @click='editComment(comments)'>Send</button>
          </div>
            </div>
           
</template>

<script>
export default {
    props:['comments',],

    data(){
        return {
             isVisible:false,
             isDelete:false,
             isEditing:false,
             isShow:true,
        }
    },
    methods: {
        showAction(e){
            this.isVisible=!this.isVisible;   
        },
        deleteComment(comments){
       this.$emit('delete-comment', comments);
       this.isDelete = !this.isDelete;
       this.isShow = !this.isShow;
       this.isVisible = !this.isVisible;
        },
        showDelete(){         
            this.isDelete=true;    
            this.isShow = false;   
        },
        hideDelete() {
            this.isDelete = false;
            this.isShow = true;           
        },
        editMessage(){
            this.isEditing = true;
            this.isDelete =false;
            this.isShow = false;
        },
        editComment(){
            this.isShow = true;
             this.isVisible= false;
            this.isDelete =false;
             this.isEditing = false;
        },
        hideEditComment() {
            this.isVisible= false;
            this.isShow = true;
            this.isEditing=false;
           
        },
    }
}
</script>

<style lang="scss" scoped>

.comments {
    &-item {
        padding: 10px 0px;
        display: flex;
        font-size: 15px;
        align-items: center;
        max-width: 100%;
        overflow: hidden;
        transition: 0.3s;
&.delete{
display:none;
}
        .item {
        &-avatar {
            margin-right: 20px;
        }
         &-info {
             display: block;
             width: 100%;
             transition: 0.3s;
           
            &_name {
                font-size: 11px;
            }
            &_text {
                font-size: 16px;
                white-space: nowrap;
               
            }
        }
        &-action {
            font-size: 11px;
            font-weight: 600;
            transition: 0.3s;
            width: 100px;
            &.hidden {
                width: 0;
                font-size: 0;
            }
            span {
                padding: 5px;
                cursor: pointer;
            }
            .edit{
                color:#2C3BFF;
                
            }
            .delete{
                color:#FF0000;
              
            }
        }
}
    }

}
</style>