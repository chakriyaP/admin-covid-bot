<template >
  <div class="con">
    <section class="details">
      <h2>รายชื่อของโรงพยาบาลที่ใช้ในระบบ</h2>
      <div>
        <v-tabs>
          <v-tab>คำถามที่พบบ่อย</v-tab>
          <v-tab>
            <a
              href="https://docs.google.com/spreadsheets/d/1oTiJrX3g4gOlMIY18-4kbu0FS_WfooQ_l0h-1UItylg/edit?resourcekey&fbclid=IwAR1zb4RiEtWG689QDjowaBZkJGwfFTC-_ZQuLVztWH6G7cWEzCnKh53TEGk#gid=736174848"
              >รายงานผล</a
            >
          </v-tab>
        </v-tabs>
      </div>

      <div
        :v-if="items"
        v-for="(item, index) in items"
        :key="index"
        class="question-con"
      >
        <div class="titel">
          <h4>หมวด {{ index }}</h4>
          <button>เพิ่มคำถาม</button>
        </div>

        <v-simple-table>
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-left">คำถาม</th>
                <th class="text-left">คำตอบ</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(i, n) in item" :key="n">
                <td>{{ n }}</td>
                <td>{{ i }}</td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </div>
      <button>เพิ่มหมวดคำถาม</button>
    </section>
  </div>
</template>
  </div>
</template>
<script>
export default {
  data() {
    return {
      items: {},
      // items: {
      //   Animal: {
      //     ใช่หมารึเปล่าา: "ไม่ใช่",
      //     "Please note that as of 2021, the syntax in MrAleister's answer":
      //       "ไม่ใช่",
      //   },
      //   "Stack Overflow": {
      //     "See the Firestore documentation": "Yes",
      //   },
      // },
    };
  },
  mounted() {
    this.initData();
  },
  computed: {
    // nameQuestion() {
    //   console.log(Object.keys(this.items));
    //   return Object.keys(this.items);
    // },
  },
  methods: {
    async initData() {
      try {
        const baseApiUrl =
          "https://asia-northeast2-line-chatbot-covid.cloudfunctions.net/api";
        const { data } = await this.$axios.get(`${baseApiUrl}/question`);

        this.items = data;
        console.log(" this.items", this.items);
      } catch (error) {
        console.log("error", error);
      }
    },
  },
};
</script>
<style lang="scss">
.con {
  width: 100vw;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;

  .details {
    display: flex;
    flex-direction: column;
    width: 80%;
    height: 100%;
    padding: 16px 0;
  }
}
.question-con {
  margin-top: 20px;
}
.titel {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  button {
    background-color: #96c5cb;
    padding: 4px 20px;
    color: white;
    border-radius: 10px;
  }
}

button {
  background-color: #96c5cb;
  padding: 6px 20px;
  color: white;
  border-radius: 10px;
  margin-top: 20px;
}

a {
  text-decoration: none;
  color: gray;
}

::v-deep .v-application a {
  color: gray;
  font-size: 3rem;
}
</style>