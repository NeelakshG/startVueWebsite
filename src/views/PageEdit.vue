<template>
  <h4>Edit {{ page.pageTitle }}</h4>
  <div class="container mb-3">
    <form action="">
      <div class="mb-3">
        <label for="" class="form-label"> Page Title </label>
        <input type="text" class="form-control" v-model="page.pageTitle" />
      </div>

      <div class="mb-3">
        <label for="" class="form-label">Link Text</label>
        <input type="text" class="form-control" v-model="page.link.text" />
      </div>

      <div class="mb-3">
        <label for="" class="form-label"> Content </label>
        <textarea
          type="text"
          class="form-control"
          rows="5"
          v-model="page.content"
        ></textarea>
      </div>

      <div class="row mb-3">
        <div class="form-check">
          <input
            class="form-check-input"
            type="checkbox"
            v-model="page.published"
          />
          <label class="form-check-label"> Published </label>
        </div>
      </div>

      <div class="mb-3">
        <button class="btn btn-primary" @click.prevent="submit">Edit</button>
        <button class="btn btn-secondary">Cancel</button>
      </div>
    </form>
  </div>
</template>

<script setup>
import { useRouter } from "vue-router";
import { inject } from "vue";

const { index } = defineProps(["index"]); //this lets you take the props without doing the whole blah
const pages = inject("$pages");
const bus = inject("$bus");

const route = useRouter();

let page = pages.getSinglePage(index);

function submit() {
  pages.editPage(index, page);

  bus.$emit("ppage-updated", {
    index,
    page,
  });
}
</script>
