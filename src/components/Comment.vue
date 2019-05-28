<template>
  <div class="comments-item">
    <template v-if="isShow">
      <div class="item-avatar">
        <img src="../assets/av-1.png" alt>
      </div>
      <transition name="show-edit">
        <div class="item-action" v-show="isVisible">
          <span class="edit" @click="editMessage">Edit</span>
          <span class="delete" @click="showDelete">Delete</span>
        </div>
      </transition>
      <div class="item-info" @click="showAction">
        <div class="item-info_name">{{comments.name}}</div>
        <div class="item-info_text">{{comments.text }}</div>
      </div>
    </template>
    <transition name="show-delete">
      <div class="delete-field" v-show="isDelete">
        <div>
          <span>Delete message?</span>
        </div>
        <div>
          <button @click="hideDelete" class="btn btn-default">No</button>
          <button @click="deleteComment(comments)" class="btn btn-danger">Yes</button>
        </div>
      </div>
    </transition>
    <transition name="show-delete">
      <div class="comments-field" v-show="isEditing">
        <input type="text" class="comments-input" v-model="comments.text" @blur="hideEditComment()">
        <button
          class="btn btn-send"
          :class="[isVisible ? '' : 'hidden']"
          @click="editComment()"
        >Send</button>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: ["comments"],

  data() {
    return {
      isVisible: false,
      isDelete: false,
      isEditing: false,
      isShow: true
    };
  },
  methods: {
    showAction() {
      this.isVisible = !this.isVisible;
    },
    deleteComment(comments) {
      this.$emit("delete-comment", comments);
      this.isDelete = !this.isDelete;
      this.isShow = !this.isShow;
      this.isVisible = !this.isVisible;
    },
    showDelete() {
      this.isDelete = true;
      this.isShow = false;
    },
    hideDelete() {
      this.isDelete = false;
      this.isShow = true;
    },
    editMessage() {
      this.isEditing = true;
      this.isDelete = false;
      this.isShow = false;
    },
    editComment() {
      this.isShow = true;
      this.isVisible = false;
      this.isDelete = false;
      this.isEditing = false;
    },
    hideEditComment() {
      this.isVisible = false;
      this.isShow = true;
      this.isEditing = false;
    }
  }
};
</script>

<style lang="scss" scoped>
.comments {
  &-item {
    padding: 10px 0px;
    height: 40px;
    display: flex;
    font-size: 15px;
    align-items: center;
    max-width: 100%;
    overflow: hidden;
    transition: 0.3s;
    &.delete {
      display: none;
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
        span {
          padding: 5px;
          cursor: pointer;
        }
        .edit {
          color: #2c3bff;
        }
        .delete {
          color: #ff0000;
        }
      }
    }
    .delete {
      &-field {
        width: 100%;
        background-color: #f4f5ff;
        display: flex;
        justify-content: space-between;
        align-items: center;
        button {
          display: inline-block;
          cursor: pointer;
          font-size: 11px;
          color: #fff;
          border-radius: 4px;
          background-color: #2c3bff;
          border: 1px solid transparent;
          padding: 17px 20px;
        }
        .btn {
          &-danger {
            background-color: #ff0000;
            &:hover {
              background-color: darken(#ff0000, 10%);
            }
          }
          &-default {
            background-color: #2c3bff;
            &:hover {
              background-color: darken(#2c3bff, 10%);
            }
          }
        }
      }
    }

    /*Animation*/
    .show-edit {
      &-enter-active,
      &-leave-active {
        transition: all 0.2s;
        width: 100px;
        transform: translateX(0px);
      }

      &-enter,
      &-leave-to {
        transform: translateX(50px);
        opacity: 0;
        width: 0;
        font-size: 0;
      }
    }

    .show-delete {
      &-enter-active,
      &-leave-active {
        transition: all 0.2s;

        transform: translateX(0px);
      }

      &-enter,
      &-leave-to {
        transform: translateX(-50px);
        opacity: 0;
      }
    }
  }
}
</style>