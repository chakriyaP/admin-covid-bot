<template >
  <div class="con">
    <section class="details">
      <h2>รายชื่อของโรงพยาบาลที่ใช้ในระบบ</h2>
      <div>
        <v-tabs>
          <v-tab>คำถามที่พบบ่อย</v-tab>
          <v-tab>
            <a
              href="https://docs.google.com/spreadsheets/d/1oTiJrX3g4gOlMIY18-4kbu0FS_WfooQ_l0h-1UItylg/edit?resourcekey&fbclid=IwAR1zb4RiEtWG689QDjowaBZkJGwfFTC-_ZQuLVztWH6G7cWEzCnKh53TEGk#gid=789109387"
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

          <!-- <v-dialog v-model="dialog" persistent max-width="600px">
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="btn" v-bind="attrs" v-on="on"> เพิ่มคำถาม </v-btn>
            </template>
            <v-card>
              <v-card-title>
                <span class="text-h5">เพิ่มคำถาม ในหมวด {{ index }}</span>
              </v-card-title>
              <v-card-text>
                <v-container>
                  <v-row>
                    <h3>คำถาม-คำตอบ</h3>
                    <v-col cols="12">
                      <v-text-field label="คำถาม" required></v-text-field>
                    </v-col>
                    <v-col cols="12" class="aser">
                      <v-text-field label="คำตอบ" required></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="dialog = false">
                  ยกเลิก
                </v-btn>
                <v-btn color="blue darken-1" text @click="dialog = false">
                  บันทึก
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog> -->
        </div>

        <v-simple-table>
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-left">คำถาม</th>
                <th class="text-center">คำตอบ</th>
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

      <v-dialog v-model="dialog" persistent max-width="600px">
        <template v-slot:activator="{ on, attrs }">
          <v-btn color="btn" dark v-bind="attrs" v-on="on">
            เพิ่มหมวดคำถาม
          </v-btn>
        </template>
        <v-card>
          <v-card-title>
            <span class="text-h5">เพิ่มหมวดคำถาม</span>
          </v-card-title>
          <v-card-text>
            <v-container>
              <v-row>
                <h3>หมวดคำถาม</h3>
                <v-col cols="12">
                  <v-text-field label="หมวดคำถาม" required></v-text-field>
                </v-col>
                <hr />
                <h3>คำถาม-คำตอบ</h3>
                <v-col cols="12">
                  <v-text-field label="คำถาม" required></v-text-field>
                </v-col>
                <v-col cols="12" class="aser">
                  <v-text-field label="คำตอบ" required></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" text @click="dialog = false">
              ยกเลิก
            </v-btn>
            <v-btn color="blue darken-1" text @click="dialog = false">
              บันทึก
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </section>
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
      dialog: false,

      // question: false,
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

.btn {
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
th {
  text-align: center;
}

::v-deep .v-application a {
  color: gray;
  font-size: 3rem;
}
::v-deep .v-application .text-h5 {
  font-family: "Kanit", sans-serif !important;
}
.aser {
  margin-top: -10px;
}
</style>