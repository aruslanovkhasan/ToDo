<template>
  <Transition name="modal">
    <div class="modal" @click="closeModal">
      <div class="modal__block" @click.stop="">
        <h2 class="modal__title">
          {{ edit ? words.titlewindowedit[lang] : words.titlewindow[lang] }}
        </h2>
        <div class="modal__inputs">
          <label for="title">
            <span>Title</span>
            <input type="text" id="title" v-model="title" />
          </label>
          <label for="content">
            <span>Content</span>
            <textarea id="content" v-model="descr"></textarea>
          </label>
        </div>
        <div class="modal__btns">
          <button class="modal__btn del" @click="closeModal">{{words.closebtn[lang]}}</button>
          <button v-if="!edit" class="modal__btn edit" @click="addNote">{{words.addbtn[lang]}}</button>
          <button v-else class="modal__btn edit" @click="changeNote">{{words.editwindowbtn[lang]}}</button>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script>
export default {
  inject: ['words'],
  data() {
    return {
      title: "",
      descr: "",
      id: this.currentId,
    };
  },
  props: {
    currentId: Number,
    edit: Boolean,
    editNote: Object,
    lang: String
  },
  methods: {
    closeModal() {
      this.$emit("closeModal", false);
      this.title = "";
      this.descr = "";
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
        this.closeModal();
      }
    },
    changeNote(){
      if (this.title != '' && this.descr != '') {
        const editedNote = {
          id: this.editNote.id,
          title: this.title,
          descr: this.descr,
          date: new Date().toLocaleDateString(),
        }
        this.$emit('editedNote', editedNote)
        this.closeModal()
      }
    }
  },
};
</script>

<style>
.modal-enter-active,
.modal-leave-active {
  transition: all 0.25s ease-out;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
  transform: scale(1.5);
}

.modal {
  background: rgba(0, 0, 0, 0.35);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 999;
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
  font-family: "RR";
  font-size: 24px;
  line-height: 32px;
  color: #1c1b1f;
  margin-bottom: 16px;
}
.modal__inputs {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
.modal__inputs label {
  position: relative;
}
.modal__inputs span {
  position: absolute;
  top: 8px;
  left: 16px;
  font-family: "RR";
  font-weight: 400;
  font-size: 12px;
  line-height: 16px;
  letter-spacing: 0.4px;
  color: #6750a4;
}
.modal__inputs input,
.modal__inputs textarea {
  border: none;
  outline: none;
  resize: none;
  width: 100%;
  background: #e7e0ec;
  border-radius: 4px 4px 0px 0px;
  padding: 23px 16px 9px;
  font-family: "RR";
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  letter-spacing: 0.5px;
  color: #49454f;
  border-bottom: 1px solid #1c1b1f;
}
.modal__btns {
  display: flex;
  justify-content: flex-end;
  gap: 8px;
  margin-top: 24px;
}
.modal__btn {
  padding: 10px 12px;
  font-size: 14px;
  line-height: 20px;
  letter-spacing: 0.1px;
  text-transform: uppercase;
}
</style>
