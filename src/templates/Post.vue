<template>
  <Layout>
    <!-- Page Header -->
    <header class="masthead" :style="`background-image: url('${GRIDSOME_API_URL+$page.post.cover.url}')`">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-heading">
              <h1>{{$page.post.title}}</h1>
              <h2 class="subheading">Problems look mighty small from 150 miles up</h2>
              <span class="meta">
                Posted by 
                <a href="#">{{$page.post.created_by.firstname}}{{$page.post.created_by.lastname}}</a>
                on {{$page.post.created_at}}
              </span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Post Content -->
    <article>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto" v-html="mdToHtml($page.post.content)">
            
          </div>
        </div>
      </div>
    </article>

    <hr />
  </Layout>
</template>
<page-query>
query($id:ID!){
  post:strapiPost(id:$id){
    id
    title
    cover{
      url
    }
    tags{
      id
      title
    }
    content
    created_by{
      firstname
      lastname
      id
    }
    created_at
  }
}
</page-query>


<script>
import MarkdownIt from 'markdown-it'
const md = new MarkdownIt()

export default {
  name: "PostDetailPage",
  methods:{
    mdToHtml(markDown){
      return md.render(markDown)
    }
  }
};
</script>

<style>
</style>