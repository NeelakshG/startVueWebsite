<template>
  <div class="container mb-3">
    <form action="">
      <div class="mb-3">
        <label class="form-label"> Page Title </label>
        <input type="text" class="form-control" v-model="pageTitle" />
      </div>

      <div class="mb-3">
        <label class="form-label"> Content </label>
        <textarea
          type="text"
          class="form-control"
          rows="5"
          v-model="content"
        ></textarea>
      </div>

      <div class="mb-3">
        <label class="form-label">Link Text</label>
        <input type="text" class="form-control" v-model="linkText" />
      </div>

      <div class="mb-3">
        <label class="form-label">Link URL</label>
        <input type="text" class="form-control" v-model="linkURL" />
      </div>

      <div class="row mb-3">
        <div class="form-check">
          <input class="form-check-input" type="checkbox" v-model="published" />
          <label class="form-check-label"> Published </label>
        </div>
      </div>

      <div class="mb-3">
        <button
          :disabled="isFormInvalid"
          class="btn btn-primary"
          @click.prevent="submitForm"
        >
          Create Page
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  emits: {
    pageCreated(pageTitle, content, link, published) {
      if (!pageTitle) {
        return false;
      }

      if (!content) {
        return false;
      }

      if (!link || !link.url || !link.text) {
        return false;
      }

      return true;
    },
  },
  computed: {
    isFormInvalid() {
      return (
        !this.pageTitle || !this.content || !this.linkText || !this.linkURL
      );
    },
  },
  data() {
    return {
      pageTitle: "",
      content: "",
      linkText: "",
      linkURL: "",
      published: true,
    };
  },
  methods: {
    submitForm() {
      if (!this.pageTitle || !this.content || !this.linkText || !this.linkURL) {
        alert("please fill out the form.");
        return;
      }

      this.$emit("pageCreated", {
        pageTitle: this.pageTitle,
        content: this.content,
        link: {
          text: this.linkText,
          url: this.linkURL,
        },
        published: this.published,
      });

      this.pageTitle = "";
      this.content = "";
      this.linkText = "";
      this.linkURL = "";
      this.published = true;
    },
  },
  watch: {
    pageTitle(newTitle, oldTitle) {
      if (this.linkText == oldTitle) {
        this.linkText = newTitle;
      }
    },
  },
};
</script>
