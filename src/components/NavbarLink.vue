<template>
  <li>
    <RouterLink
      :to="`/${index}`"
      class="nav-link"
      active-class="active"
      aria-current="page"
      v-bind:href="page.link.url"
      :title="`this link goes to the ${page.link.text} page`"
      >{{ page.link.text }}</RouterLink
    >
  </li>
</template>

<script>
export default {
  props: ["page", "index"],
};
</script>
