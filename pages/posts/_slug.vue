<template>
  <div>
  <Header :title=post.title />
    <div class="container">
      <div class="row">
        <div class="col-lg-8">
          <nav aria-label="breadcrumb" class="mt-4">
            <ol class="breadcrumb">
              <li class="breadcrumb-item"><nuxt-link to="/">Главная</nuxt-link></li>
              <li class="breadcrumb-item active" aria-current="page">{{ post.title }}</li>
            </ol>
          </nav>
          <img class="img-fluid rounded " :src="post.image" alt="">
          <hr>
          <p v-html="post.content"></p>
          <div class="d-flex justify-content-end">
            <span v-for="tag in post.tags">
                  <nuxt-link :to="`/tags/${tag}`" class="mr-1 badge badge-info">#{{ tag }}</nuxt-link>
            </span>
          </div>
          <hr>
          <div class="d-flex">
            <div class="mr-auto p-2 lead">Автор: {{ post.author }}</div>
            <div class="p-2">Опубликовано: {{ post.created_at }}</div>
          </div>
          <hr>
          <Comments :comments="comments" :post="post"/>
        </div>
        <Aside :tags=tags :aside=aside />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import post_detail from "@/layouts/post_detail";
import Header from "~/components/Header";
import Aside from "@/components/Aside";
import Comments from "@/components/Comments";
export default {
  components: {
    Aside,
    Header,
    Comments
  },
  layout: "post_detail",
  async asyncData({params}) {
    const post = await axios.get(`http://127.0.0.1:8000/api/posts/${params.slug}`);
    const tags = await axios.get(`http://127.0.0.1:8000/api/tags/`);
    const aside = await axios.get(`http://127.0.0.1:8000/api/aside/`);
    const comments = await axios.get(`http://127.0.0.1:8000/api/comments/${params.slug}`);
    return {
      post: post.data,
      tags: tags.data,
      aside: aside.data,
      comments: comments.data
    }
  },
}
</script>

<style scoped>

</style>