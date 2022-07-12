<template>
  <transition name="scale">
    <div class="modal" @click="closeModal">
      <div class="modal__block" @click.stop="">
        <h3 class="modal__title"> 
          {{ edit ? words.titlewindowedit[lang] : words.titlewindow[lang] }}
        </h3>
        <div class="modal__inputs">
          <label>
            <span>Title</span>
            <input v-model="title" type="text" />
          </label>
          <label>
            <span>Content</span>
            <textarea v-model="descr"></textarea>
          </label>
        </div>
        <div class="modal__btns">
          <button class="btn red" @click="closeModal">{{ words.closebtn[lang] }}</button>
          <button v-if="!edit" class="btn purple" @click="addNote">
            {{ words.addbtn[lang] }}
          </button>
          <button v-else class="btn purple" @click="changeNote">
            {{ words.editwindowbtn[lang] }}
          </button>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      descr: "",
      id: this.currentId,
    };
  },
  props: {
    lang: String,
    edit: {
      typeof: Boolean,
    },
    currentId: {
      typeof: Number,
    },
    editNote: {
      typeof: Object,
    },
  },
  inject: ['words'],
  methods: {
    closeModal() {
      this.$emit("closeModal", false);
      this.title = '';
      this.descr = '';
    },
    addNote() {
      if (this.title != "" && this.descr != "") {
        const item = {
          id: this.id++,
          title: this.title,
          descr: this.descr,
          date: new Date().toLocaleDateString(),
        };
        this.$emit("addNote", item);
        this.$emit("close", false);
        this.title = "";
        this.descr = "";
      }
    },
    changeNote() {
      if (this.title != "" && this.descr != "") {
        const editedNote = {
          id: this.editNote.id,
          title: this.title,
          descr: this.descr,
          date: new Date().toLocaleDateString(),
        };
        this.$emit("editedNote", editedNote);
        this.closeModal();
        this.title = "";
        this.descr = "";
      }
    },
  },
};
</script>

<style>
.modal {
  background: rgba(0, 0, 0, 0.35);
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  z-index: 9999;
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal__block {
  max-width: 312px;
  width: 100%;
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.11),
      rgba(103, 80, 164, 0.11)
    ),
    #fffbfe;
  border-radius: 28px;
  padding: 24px;
}
.modal__title {
  font-size: 24px;
  line-height: 32px;
  margin-bottom: 15px;
}
.modal__inputs {
  display: flex;
  flex-direction: column;
  gap: 15px;
}
.modal__inputs label {
  position: relative;
}
.modal__inputs span {
  font-size: 12px;
  line-height: 16px;
  color: #6750a4;
  position: absolute;
  top: 8px;
  left: 16px;
}
.modal__inputs input,
.modal__inputs textarea {
  background: #e7e0ec;
  border-radius: 4px 4px 0px 0px;
  border: none;
  outline: none;
  padding: 23px 0 16px 9px;
  font-size: 16px;
  line-height: 24px;
  resize: none;
  display: block;
  width: 100%;
  border-bottom: 1px solid #1c1b1f;
}
.modal__btns {
  margin-top: 25px;
  display: flex;
  gap: 10px;
  justify-content: flex-end;
}
.btn {
  font-size: 14px;
  line-height: 20px;
  text-transform: uppercase;
  padding: 12px;
  background: transparent;
  border-radius: 5px;
}
.red {
  color: #cf1b1b;
  transition: background 300ms;
}
.red:hover {
  background: rgba(207, 27, 27, 0.261);
}
.purple {
  color: #6750a4;
  transition: background 300ms;
}
.purple:hover {
  background: rgba(102, 80, 164, 0.302);
}

.scale-enter-active,
.scale-leave-active {
  transition: all 0.2s linear;
}

.scale-enter-from,
.scale-leave-to {
  transform: scale(1.5);
  opacity: 0;
}
</style>