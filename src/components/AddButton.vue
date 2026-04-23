<template>
  <button class="add__btn" @click="$emit('openModal')">
    <img src="@/assets/img/edit.svg" alt="" />
  </button>
</template>

<script>
export default {};
</script>

<style>
.add__btn {
  position: fixed;
  right: 30px;
  bottom: 30px;
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.11),
      rgba(103, 80, 164, 0.11)
    ),
    #fffbfe;
  border-radius: 16px;
  padding: 19px;
  box-shadow: 0px 4px 8px 3px rgba(0, 0, 0, 0.15);
  filter: drop-shadow(0px 1px 3px rgba(0, 0, 0, 0.3));
  width: 56px;
  height: 56px;
}
</style>
