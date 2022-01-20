<template>
  <a href="javascript: alert('+++');">
    <div class="addCard">
      <i class="fas fa-plus pluss"></i>
      <p>เพิ่มโรงพยาบาล</p>
    </div>
  </a>
</template>

<script>
export default {
  name: "HospitalAdd",
  props: {},
};
</script>

<style scoped>
.addCard {
  width: 220px;
  height: 200px;
  border: 2px solid var(--gray-color);
  border-radius: 12px;
  color: var(--green-color);
  background-color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.addCard i {
  font-size: 36px;
  padding-bottom: 12px;
}
</style>
