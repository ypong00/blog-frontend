<template>
  <Layout>
    <!-- Page Header-->
    <header
     class="masthead"
     :style="{
       backgroundImage: `url(${GRIDSOME_API_URL + $page.allStrapiGeneral.edges[0].node.cover.url})`
     }">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{ $page.allStrapiGeneral.edges[0].node.title }}</h1>
              <span class="subheading">
                  {{ $page.allStrapiGeneral.edges[0].node.subtitle }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content-->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div
            class="post-preview"
            v-for="edge in $page.posts.edges"
            :key="edge.node.id"
          >
            <g-link :to="`/posts/${edge.node.id}`">
              <h2 class="post-title">
                {{ edge.node.title }}
              </h2>
            </g-link>
            <p class="post-meta">
              Posted by
              <a href="#!">
                {{ edge.node.create_by }}
              </a>
              on {{ edge.node.created_at }}
            </p>
            <p>
              <span v-for="tag in edge.node.tags" :key="tag.id">
                <g-link :to="'/tags/' + tag.id">
                  {{ tag.title }}
                </g-link>
                &nbsp;&nbsp;
              </span>
            </p>
          </div>
          <hr />
          <!-- Pager-->
          <!-- <div class="clearfix">
                    <a class="btn btn-primary float-right" href="#!">
                        Older Posts →
                    </a>
                </div> -->
          <Pager :info="$page.posts.pageInfo" />
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query ($page: Int) {
  posts: allStrapiPost (perPage: 2, page: $page) @paginate {
    pageInfo {
      totalPages,
      currentPage
    }
    edges {
      node {
        id
        title
        tags {
          id,
          title,
        },
        created_at,
        create_by
      }
    }
  }

  allStrapiGeneral {
      edges {
          node {
              id,
              title,
              subtitle,
              cover {
                  url
              }
          }
      }
  }
}
</page-query>

<script>
import { Pager } from "gridsome";

export default {
  metaInfo: {
    title: "Hello, world!",
  },
  name: "HomePage",
  components: {
    Pager,
  },
};
</script>

<style>
</style>
