<template>
<div>
    <h3 v-if="this.$route.params.semester == 'spring'">spring</h3>
    <h3 v-else>fall</h3>
    <table class="container">
      <tr>
        <th>Code</th>
        <th>Title</th>
        <th>Semester</th>
        <th>Credits</th>
        <th>Description</th>
      </tr>
      <tr id="item" v-for="course in semester" :key="course.id">
        <td>{{ course.code }}</td>
        <td>{{ course.title }}</td>
        <td>{{ course.semester }}</td>
        <td>{{ course.credits }}</td>
        <td v-if="course.description == ''">No course description is provided</td>
        <td v-else>{{ course.description }}</td>
      </tr>
    </table>
    <a href="/">Back to courses</a>
</div>
</template>

<script>
export default {
    name: "Semester",
    data() {
        return {
        semester: [],
        };
    },
    methods: {
    fetchSemester(semester) {
        fetch(`http://localhost:3000/api/semesters/${semester}`)
        .then((response) => response.json())
        .then((data) => (this.semester = data))
        .catch((err) => console.log(err.message));
        }
    },
    mounted() {
        this.fetchSemester(this.$route.params.semester);
        console.log("mounted");
    },
};
</script>

<style scoped>
th {
    background: rgb(100, 151, 122);
    margin-bottom: 5px;
    padding: 8px 4vw;
  }
  td {
    background: rgb(186, 228, 204);
    margin-bottom: 5px;
    padding: 8px 2.5vw;
  }
  th, td {
    font-size: 15px;
  }
  .container {
    background: #d5d7d8;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
    margin: auto;
    margin-bottom: 30px;
    padding: 10px 50px;
    display: flex;
    justify-content: space-evenly;
    flex-direction: column;
  }
</style>