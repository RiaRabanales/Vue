<template>
  <div class="post">
    <router-link :to="{ name: 'Details', params: { id: post.id } }">
      <h3>{{ post.title }}</h3>
    </router-link>
    <p>{{ snippet }}</p>
    <span v-for="tag in post.tags" :key="tag" @click="goToTag(tag)"> #{{ tag }} </span>
  </div>
</template>

<script>
import { computed } from "vue";
import { useRouter } from 'vue-router'

export default {
  props: ["post"],
  setup(props) {
    const router = useRouter();

    const snippet = computed(() => {
      return props.post.body.substring(0, 100) + "....";
      //así recupero sólo el principio del texto del post
    });

    const goToTag = (tag) => {
      let route = "/tags/" + tag;
      router.push({ path: route });
    };

    return { snippet, goToTag };
  },
};
</script>

<style>
.post {
  margin: 0 22px 30px;
  padding-bottom: 22px;
  border-bottom: 1px dashed #e7e7e7;
}
.post h3 {
  display: inline-block;
  position: relative;
  font-size: 26px;
  color: white;
  margin-bottom: 10px;
  max-width: 400px;
}
.post h3::before {
  content: "";
  display: block;
  width: 100%;
  height: 100%;
  background: #ff8800;
  position: absolute;
  z-index: -1;
  padding-right: 40px;
  left: -30px;
  transform: rotateZ(-1deg);
}
.post span {
  color: rgb(163, 163, 163);
  margin-right: 3px;
  cursor: pointer;
}
</style>