<template>
  <div class="course-container">
    <h2>📚 รายละเอียดการเรียน</h2>

    <div class="course-card">
      <ul class="course-list">
        <li v-for="course in courses" :key="course.id" class="course-item">
          <span>
            {{ course.code }} - {{ course.name }} ({{ course.credit }} หน่วยกิต) - เกรด: {{ course.grade }}
          </span>
          <div>
            <button class="btn-edit" @click="editCourse(course)">แก้ไข</button>
            <button class="btn-delete" @click="deleteCourse(course.id)">ลบ</button>
          </div>
        </li>
      </ul>

      <h4 class="mt-3">➕ เพิ่มวิชา</h4>
      <form @submit.prevent="addCourse" class="course-form">
        <input v-model="newCourse.code" placeholder="รหัสวิชา" required />
        <input v-model="newCourse.name" placeholder="ชื่อวิชา" required />
        <input v-model="newCourse.credit" type="number" placeholder="หน่วยกิต" required />
        <input v-model="newCourse.grade" placeholder="เกรด" required />
        <button class="btn-add">เพิ่ม</button>
      </form>

      <!-- ฟอร์มแก้ไขวิชา -->
      <div v-if="editingCourse" class="edit-container">
        <h4>📝 แก้ไขวิชา</h4>
        <input v-model="editingCourse.code" placeholder="รหัสวิชา" />
        <input v-model="editingCourse.name" placeholder="ชื่อวิชา" />
        <input v-model="editingCourse.credit" type="number" placeholder="หน่วยกิต" />
        <input v-model="editingCourse.grade" placeholder="เกรด" />
        <button class="btn-save" @click="updateCourse">บันทึก</button>
        <button class="btn-cancel" @click="editingCourse = null">ยกเลิก</button>
      </div>
    </div>
  </div>
</template>

<script>
import "@/assets/course.css";

export default {
  data() {
    return {
      courses: [],
      newCourse: { code: "", name: "", credit: "", grade: "" },
      editingCourse: null,
    };
  },
  mounted() {
    this.fetchCourses();
  },
  methods: {
    fetchCourses() {
      fetch("http://localhost:3000/courses")
        .then((res) => res.json())
        .then((data) => {
          this.courses = data;
        });
    },
    addCourse() {
      fetch("http://localhost:3000/courses", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(this.newCourse),
      }).then(() => {
        this.newCourse = { code: "", name: "", credit: "", grade: "" };
        this.fetchCourses();
      });
    },
    deleteCourse(id) {
      fetch(`http://localhost:3000/courses/${id}`, { method: "DELETE" }).then(() => {
        this.fetchCourses();
      });
    },
    editCourse(course) {
      this.editingCourse = { ...course };
    },
    updateCourse() {
      fetch(`http://localhost:3000/courses/${this.editingCourse.id}`, {
        method: "PUT",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(this.editingCourse),
      }).then(() => {
        this.editingCourse = null;
        this.fetchCourses();
      });
    },
  },
};
</script>
