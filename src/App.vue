<template>
  <div id="app">
    <div class="navbar">
      <div class="container">
        <div class="nav-icon">
          <i class="el-icon-menu"></i>
        </div>
        <div class="nav-brand"><a href="#">แบบทดสอบ</a></div>
      </div>
    </div>
    <div class="main">
      <div class="container">
        <el-card>
          <div class="card-title">เขียนหน้าเว็บแสดงเบอร์โทรศัพท์</div>
          <el-row>
            <el-col :span="20" :offset="2">
              <el-form ref="form_submit" class="form-submit">
                <el-form-item label="1.) เบอร์โทรที่ไม่มี 0 นำหน้า">
                  <el-tooltip effect="dark">
                    <div slot="content">
                      <span>- ให้ขีดอยู่ที่ index 2 และ 6 </span><br />
                      <span>- ขีดต้องขึ้นมาระหว่างพิมพ์ </span><br />
                      <span
                        >- เมื่อกรอกจำนวนตัวเลขมากกว่า 9
                        ให้เบอร์โทรไม่มีขีด</span
                      ><br>
                      <span>- กรณีลบเบอร์ให้ลบขีดทิ้งอัตโนมัติ</span>
                    </div>
                    <el-input
                      clearable
                      @input="phoneFormatShort"
                      v-model="phone1"
                    ></el-input>
                  </el-tooltip>
                </el-form-item>
                <el-form-item label="2.) เบอร์โทรที่มี 0 นำหน้า">
                  <el-tooltip effect="dark">
                    <div slot="content">
                      <span>- ให้ขีดอยู่ที่ index 3 และ 7</span><br>
                      <span>- ขีดต้องขึ้นมาระหว่างพิมพ์</span><br>
                      <span>- เมื่อกรอกจำนวนตัวเลขมากกว่า 10 ให้เบอร์โทรไม่มีขีด</span><br>
                      <span>- กรณีลบเบอร์ให้ลบขีดทิ้งอัตโนมัติ</span>
                    </div>
                    <el-input
                      clearable
                      @input="phoneFormatFull"
                      v-model="phone2"
                    ></el-input>
                  </el-tooltip>
                </el-form-item>
                <el-form-item>
                  <el-button type="primary" class="btn-submit" @click="submitForm"
                    >Submit</el-button
                  >
                </el-form-item>
              </el-form>
            </el-col>
          </el-row>
        </el-card>
      </div>
    </div>
    <div class="footer">
      <div class="container">
        <span>Copyright 2023 &copy;KITSADA_PHOSON</span> 
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  mounted() {
    console.log("welcome to website");
  },
  data() {
    return {
      phone1: "",
      phone2: "",
    };
  },
  methods: {
    submitForm() {
      this.$alert(
        `<p>1.) เบอร์โทรที่ไม่มี 0 นำหน้า : ${this.phone1} <br> 2.) เบอร์โทรที่มี 0 นำหน้า : ${this.phone2}</p>`,
        "!สำเร็จ",
        {
          dangerouslyUseHTMLString: true,
          confirmButtonText: "OK",
        }
      );
    },
    phoneFormatShort() {
      const phoneValue = this.phone1.replace(/\D/g, "");
      if (!!phoneValue && phoneValue[0] == 0) {
        this.phone1 = "";
      } else {
        this.phone1 = this.appendDash(phoneValue);
      }
    },
    phoneFormatFull() {
      const phoneValue = this.phone2.replace(/\D/g, "");
      this.phone2 = this.appendDash(phoneValue, false);
    },

    appendDash(value, short = true) {
      var phoneValue = "";
      for (let i = 0; i < value.length; i++) {
        if (i == (short ? 2 : 3) || i == (short ? 5 : 6)) phoneValue += "-";
        phoneValue += value[i];
      }

      if (
        (short && phoneValue.length > 11) ||
        (!short && phoneValue.length > 12)
      )
        phoneValue = phoneValue.replace(/-/g, "");
      return phoneValue;
    },
  },
};
</script>
