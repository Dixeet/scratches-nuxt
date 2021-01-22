<template>
  <div>
    <p>Test</p>
    <br />
    <h1>{{ posts[0].title }}</h1>
    <markdown :md="posts[0].content" />
    <markdown :md="posts[1].content" />
  </div>
</template>

<script>
export default {
  name: 'HomePage',

  async asyncData({ $strapi }) {
    const posts = await $strapi.find('posts');

    return {
      posts,
    };
  },
};
</script>
