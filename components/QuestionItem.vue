<template>
  <tr>
    <td style="text-align: center">{{ no }}</td>
    <td>{{ question }}</td>
    <td>{{ answer }}</td>
    <td style="text-align: center">
      <img :src="image" alt="" />
    </td>
  </tr>
</template>

<script>
export default {
  name: "QuestionItem",
  props: {
    no: Number,
    question: String,
    answer: String,
    image: String,
  },
};
</script>

<style scoped>
.table img {
  width: max(150px, 90%);
  height: 150px;
  object-fit: cover;
  margin: 6px;
  border-radius: 8px;
}
</style>
