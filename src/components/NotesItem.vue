<template>
  <div class="notes__item" >
    <div class="notes__item-top" :class="{active: !grid}">
      <h3 class="notes__item-title">{{ note.title }}</h3>
      <p class="notes__item-date">{{ note.date }}</p>
    </div>
    <p class="notes__item-text">
     {{ note.descr}}
    </p>
    <div class="notes__item-btns">
      <button class="notes__item-btn edit" @click="$emit('changeNote', note.id)">
        <img src="@/assets/img/edit.svg" alt="" />
        <span>{{words.editbtn[lang]}}</span>
      </button>
      <button class="notes__item-btn del" @click="$emit('delNote', note.id)">
        <img src="@/assets/img/del.svg" alt="" />
        <span>{{words.deledit[lang]}}</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  inject: ['words'],
  props: ['grid', 'note', 'lang']
};
</script>

<style>
.notes__item {
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.05),
      rgba(103, 80, 164, 0.05)
    ),
    #fffbfe;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.3),
    0px 1px 3px 1px rgba(0, 0, 0, 0.15);
  border-radius: 16px;
  padding: 16px;
}
.notes__item-top {
  margin-bottom: 16px;
}
.notes__item-title {
  font-size: 16px;
  line-height: 24px;
  letter-spacing: 0.1px;
  color: #1c1b1f;
}
.notes__item-date {
  font-family: "RR";
  font-size: 14px;
  line-height: 20px;
  letter-spacing: 0.25px;
  color: #cac4d0;
}
.notes__item-text {
  font-family: "RR";
  font-size: 14px;
  line-height: 20px;
  letter-spacing: 0.25px;
  color: #49454f;
}
.notes__item-btns {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  margin-top: 17px;
}
.notes__item-btn {
  font-size: 14px;
  line-height: 20px;
  letter-spacing: 0.1px;
  text-transform: uppercase;
  padding: 12px;
  display: flex;
  align-items: center;
  gap: 13px;
}
.edit {
  color: #6750a4;
  transition: 0.3s;
}
.del {
  color: #cf1b1b;
  transition: 0.3s;
}
.del:hover {
  background: #ffe1e1;
  border-radius: 5px;
}
.edit:hover {
  background: #e6ddff;
  border-radius: 5px;
}
.notes__item-top.active{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
@media (max-width: 768px){
  .notes__item-btn{
    font-size: 11px;
    padding: 8px;
  }
}
</style>
