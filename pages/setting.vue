<template >
  <div class="con">
    <section class="details">
      <h1>ตั้งค่าผู้ดูแลระบบ</h1>
      <v-simple-table>
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-center">ลำดับ</th>

              <th class="text-center">ชื่อผู้ใช้งาน</th>
              <th class="text-center">บทบาท</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, index) in user" :key="index" class="text-center">
              <td>{{ index + 1 }}</td>
              <td>{{ item.user }}</td>
              <td>{{ item.role }}</td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
      <v-dialog v-model="dialog" persistent max-width="600px">
        <template v-slot:activator="{ on, attrs }">
          <v-btn color="btn" dark v-bind="attrs" v-on="on" class="mt-4">
            เพิ่มผู้ดูแลระบบ
          </v-btn>
        </template>
        <v-card>
          <v-card-title>
            <span class="text-h5">เพิ่มผู้ดูแลระบบ</span>
          </v-card-title>
          <v-card-text>
            <v-container>
              <v-row>
                <v-col cols="12">
                  <v-text-field label="ชื่อผู้ใช้งาน" required></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-text-field label="รหัสผ่าน" required></v-text-field>
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
              เพิ่มผู้ดูแลระบบ
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
      user: [
        { user: "user1", role: "โรงพยาบาลศรีนครินทร์" },
        { user: "user2", role: "โรงพยาบาลศรีนครินทร์" },
        { user: "user3", role: "โรงพยาบาลศรีนครินทร์" },
        { user: "user4", role: "โรงพยาบาลศรีนครินทร์" },
      ],
      dialog: false,
    };
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
</style>