<template>
  <div class="carousel-wrapper">
    <client-only>
      <carousel v-bind="options">
        <slide v-for="i in 5" :key="i" class="img-wrapper">
          <img :src="`./${i}-200x100.jpg`" />
        </slide>
      </carousel>
    </client-only>

    <h1 style="text-align: center">{{ title }}</h1>
    <ul>
      <li
        style="list-style-type: none; text-align: center"
        v-for="mountain in mountains"
        :key="mountain.title"
      >
        <NuxtLink
          :to="{ name: 'mountains-slug', params: { slug: mountain.slug } }"
        >
          {{ mountain.title }}
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      options: {
        loop: true,
        perPage: 3,
        paginationEnabled: false,
      },
    };
  },
};
</script>

<style lang="scss">
.carousel-wrapper {
  padding: 40px;
  height: 150px;
  .VueCarousel-slide {
    text-align: center;
  }
}
.img-wrapper img {
  margin: auto;
  width: 200px;
  height: 100px;
  background-image: linear-gradient(gray 100%, transparent 0);
}
</style>

<script>
export default {
  data() {
    return {
      title: "Important Places!",
    };
  },
  head() {
    return {
      title: this.title,
      meta: [
        {
          hid: "description",
          name: "description",
          content:
            "The amazing Nuxt application that teaches me all the cool features of Nuxt",
        },
      ],
    };
  },
  async asyncData() {
    const mountains = await fetch("https://api.nuxtjs.dev/mountains").then(
      (res) => res.json()
    );
    return { mountains };
  },
};
</script>
