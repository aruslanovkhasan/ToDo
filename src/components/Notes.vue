<template>
  <div class="notes">
    <div class="container">
      <div class="notes__top">
        <h2 class="notes__title">
          {{ notes.length > 0 ? words.infobar[lang] : words.noinfobar[lang] }}
        </h2>
        <button class="notes__btn" @click="grid = !grid">
          <img src="@/assets/img/list.svg" alt="" v-if="grid"/>
          <img src="@/assets/img/grid.svg" alt="" v-else/>
          <span>{{ grid ? words.list[lang] : words.grid[lang] }}</span>
        </button>
      </div>
      <div class="notes__list" :class="{active: !grid}">
        <NotesItem 
        :grid="grid"
        v-for="note in notes"
        :key="note.id"
        :note="note"
        @delNote="$emit('delNote', note.id)"
        @changeNote="$emit('changeNote', note.id)"
        :lang="lang"
        />
      </div>
    </div>
  </div>
</template>

<script>
import NotesItem from "@/components/NotesItem.vue";
export default {
  inject: ['words'],
  components:{
    NotesItem
  },
  data(){
    return{
      grid: true
    }
  },
  props:{
    notes: Array,
    lang: String
  }
};
</script>

<style>
.notes {
  padding-top: 30px;
}
.notes__top {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.notes__title {
  font-family: "RR";
  font-size: 22px;
  line-height: 28px;
  color: #323232;
}
.notes__btn {
  width: 121px;
  height: 56px;
  background: linear-gradient(0deg,rgba(103, 80, 164, 0.11),rgba(103, 80, 164, 0.11)),#fffbfe;
  box-shadow: 0px 4px 8px 3px rgba(0, 0, 0, 0.15),0px 1px 3px rgba(0, 0, 0, 0.3);
  border-radius: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
}
.notes__btn span {
  font-size: 14px;
  line-height: 20px;
  letter-spacing: 0.1px;
  color: #6750a4;
}

.notes__list{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  margin-top: 30px;
}

.notes__list.active{
  grid-template-columns: 1fr;
}
@media (max-width: 1024px){
  .notes__list{
    grid-template-columns: repeat(2, 1fr);
  }
}
@media (max-width: 576px){
  .notes__list{
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
