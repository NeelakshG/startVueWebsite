<template>
  <h4>Pages</h4>
  <div class="text-end">
    <router-link to="/pages/create" class="btn btn-primary btn-sm"
      >New Page</router-link
    >
  </div>
  <table class="table table-hover">
    <thead>
      <tr>
        <th>Title</th>
        <th>Link Text</th>
        <th>Is Published</th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="(page, index) in $pages.getAllPages()"
        :key="index"
        @click="goToPage(index)"
      >
        <td>{{ page.pageTitle }}</td>
        <td>{{ page.link.text }}</td>
        <td>{{ page.published ? "yes" : "no" }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
import { ref, reactive, inject } from "vue";
import { useRouter } from "vue-router";

const counter = ref(0); // {value: 0}
const data = reactive({ counter: 0 });
const router = useRouter();
const $pages = inject("$pages");

function click() {
  //counter.value++;
  data.counter++;
}

// export default {
//   data() {
//     return {
//       counter: 0,
//     };
//   },
//   methods: {
//     click() {
//       this.counter++;
//     },
//   },
// };

function goToPage(index) {
  router.push({ path: `pages/${index}/edit` });
}
</script>

<style scope>
.table.table-hover tr:hover {
  cursor: pointer;
}
</style>
