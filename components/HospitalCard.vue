<template>
  <a v-bind:href="url">
    <div class="card">
      <img v-bind:src="image" alt="Hospital" />
      <div>
        <p>{{ name }} {{ province }}</p>
      </div>
    </div>
  </a>
</template>

<script>
export default {
  name: "HospitalCard",
  props: {
    url: String,
    image: String,
    name: String,
    province: String,
  },
};
</script>

<style scoped>
a {
  color: black;
  text-decoration: none;
}

.card {
  width: 220px;
  height: 200px;
  background-color: #e5e5e5;
  border: 2px solid #e5e5e5;
  border-radius: 12px;
  text-align: left;
}
.card:hover {
  opacity: 0.8;
}

.card img {
  width: 100%;
  height: 140px;
  object-fit: cover;
  border-radius: 12px 12px 0px 0px;
}

.card p {
  margin: 0px;
  padding-left: 10px;
}
p {
  color: black;
}
p:hover {
  opacity: 0.8;
}
</style>
