<template>
  <div class="container mt-4">
    <!-- รูปภาพนิสิต -->
    <div class="row image-container">
      <div class="col-4 img-col" v-for="(img, index) in student.images" :key="index">
        <img :src="img" class="img-fluid student-img" />
      </div>
    </div>

    <!-- ข้อมูลนิสิต -->
    <div class="card mt-4 shadow-lg student-card">
      <div class="card-header">
        <h2 class="">ข้อมูลนิสิต</h2>
      </div>
      <div class="card-body">
        <div v-if="!isEditing">
          <p><strong>ชื่อ:</strong> {{ student.firstName }} {{ student.lastName }}</p>
          <p><strong>รหัสนิสิต:</strong> {{ student.studentId }}</p>
          <p><strong>สาขา:</strong> {{ student.major }}</p>
          <p><strong>จบจากโรงเรียนเดิม:</strong> {{ student.school }}</p>
          <button class="btn btn-warning w-100" @click="startEditing">แก้ไขข้อมูล</button>
        </div>

        <div v-else>
          <input v-model="student.firstName" class="form-control mb-2" placeholder="ชื่อ" />
          <input v-model="student.lastName" class="form-control mb-2" placeholder="นามสกุล" />
          <input v-model="student.studentId" class="form-control mb-2" placeholder="รหัสนิสิต" />
          <input v-model="student.major" class="form-control mb-2" placeholder="สาขา" />
          <input v-model="student.school" class="form-control mb-2" placeholder="โรงเรียน" />
          <div class="d-flex">
            <button class="btn btn-success flex-fill me-2" @click="saveEdit">บันทึก</button>
            <button class="btn btn-secondary flex-fill" @click="cancelEdit">ยกเลิก</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import "@/assets/student.css"; 
export default {
  data() {
    return {
      student: {
        firstName: "พัทธดนย์",
        lastName: "อาจหาญ",
        studentId: "6630250273",
        major: "วิทยาการคอมพิวเตอร์",
        school: "อ่างศิลาพิทยาคม",
        images: ["/images/m1.jpeg", "/images/m2.jpg", "/images/m3.jpg"],
      },
      isEditing: false,
    };
  },
  methods: {
    startEditing() {
      this.isEditing = true;
    },
    saveEdit() {
      this.isEditing = false;
    },
    cancelEdit() {
      this.isEditing = false;
    },
  },
};
</script>


