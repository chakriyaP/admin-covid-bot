<template>
  <div class="con">
    <section class="details">
      <h2>รายชื่อของโรงพยาบาลที่ใช้ในระบบ</h2>
      <div class="hosp">
        <HospitalCard
          v-for="item in list"
          :key="item.id"
          :url="item.url"
          :image="item.image"
          :name="item.name"
          :province="item.province"
        />
        <div>
          <button @click="addHospital()">เพิ่มโรงพยาบาล</button>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import router from "../layouts/router";
export default {
  name: "IndexPage",
  data() {
    return {
      list: [
        {
          id: 1,
          url: "./question",
          image:
            "https://www.smckku.com/wp-content/uploads/2019/12/smc_building.jpg",
          name: "โรงพยาบาลศรีนครินทร์",
          province: "ขอนแก่น",
        },
      ],
    };
  },
  methods: {
    addHospital() {
      this.$router.push("/create-hospital");
    },
  },
};
</script>
<style scoped>
.con {
  width: 100vw;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
:root {
  --green-color: #047684;
  --gray-color: #727272;
  --lightgray-color: #e5e5e5;
}

* {
  margin: 0;
  padding: 0;
  font-family: "Kanit", sans-serif;
}

html {
  height: 100%;
}

body {
  min-height: 100%;
}

a {
  color: black;
  text-decoration: none;
}

a:hover {
  color: inherit;
  text-decoration: inherit;
}

main {
  display: flex;
  height: 100%;
  padding: 6px;
}

/* ========== ========== */

.details {
  display: flex;
  flex-direction: column;
  width: 80%;
  height: 100%;
  padding: 8px 0 0 8px;
}

.details h2 {
  margin: 0 0 12px 0;
}

.hosp {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  padding-left: 16px;
}

.hosp a {
  margin: 0 16px 16px 0;
}
button {
  width: 220px;
  height: 200px;
  border: 1px #727272 solid;
  border-radius: 6px;
}
</style>
