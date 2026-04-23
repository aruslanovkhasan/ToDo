<template>
  <header class="header">
    <Transition name="notes">
      <div class="header__notes" v-if="header === true">
        <button @click="changeLang" class="header__lang" v-if="lang == 'ru' ">UZ</button>
        <button @click="changeLang" class="header__lang" v-else>RU</button>
        <h1 class="header__title">
          {{ words.appbartitle[lang] }}
        </h1>
        <button class="header__search">
          <img src="@/assets/img/icon.svg" alt="" @click="header = false" />
        </button>
      </div>
      <div class="header__form" v-else-if="header === false">
        <button class="header__back">
          <img src="@/assets/img/back.svg" alt="" @click="header = true" />
        </button>
        <input
          type="text"
          class="header__input"
          :placeholder="words.appbarseacrch[lang]"
          v-model="search"
        />
        <button class="header__close" @click="clearSearch">
          <img src="@/assets/img/clear.svg" alt="" />
        </button>
      </div>
    </Transition>
  </header>
</template>

<script>
export default {
  props: ['lang'],
  inject: ['words'],
  data() {
    return {
      header: true,
      search: "",
    };
  },
  watch:{
     search(val){
      this.$emit('searchValue', val);
     }
  },
  methods: {
    changeLang() {
      this.$emit('changeLang', this.lang == 'ru' ? 'uz' : 'ru');
    },
    clearSearch() {
    this.search = "";
  }
  }
};
</script>

<style>
.notes-enter-active,
.notes-leave-active {
  transition: all 0.25s ease-out;
}

.notes-enter-from {
  transform: translateY(150px);
}

.notes-leave-to {
  transform: translateY(-150px);
}

.header {
  background: #f3edf7;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25), 0px 1px 3px rgba(0, 0, 0, 0.3);
  height: 70px;
  position: relative;
  overflow: hidden;
}
.header__notes,
.header__form {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  padding: 18px 20px;
}
.header__lang {
  font-size: 22px;
  font-weight: 700;
}
.header__title {
  font-weight: 700;
  font-size: 22px;
  line-height: 28px;
  text-align: center;
  color: #1c1b1f;
}
.header__input {
  font-family: "RR";
  border: none;
  background: transparent;
  outline: none;
  width: 90%;
  font-size: 16px;
  line-height: 20px;
  color: #9d9d9d;
}
</style>
