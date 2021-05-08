<template>
  <Layout>
    <div>
      <h1>Posts2</h1>
      <ul>
        <li v-for="edge in $page.posts.edges" :key="edge.node.id">
          <g-link :to="edge.node.path">{{ edge.node.title }}</g-link>
        </li>
      </ul>
      <nav aria-label="Page navigation example">
        <ul class="pagination">
          <li class="page-item"><a class="page-link" href="#">Previous</a></li>
          <li class="page-item"><a class="page-link" href="#">1</a></li>
          <li class="page-item"><a class="page-link" href="#">2</a></li>
          <li class="page-item"><a class="page-link" href="#">3</a></li>
          <li class="page-item"><a class="page-link" href="#">Next</a></li>
        </ul>
      </nav>
      <Pager
        class="pager"
        :info="$page.posts.pageInfo"
        nav-class="navigation"
        link-class="page-link page-item"
        activeLink-class="active"
      />
    </div>
  </Layout>
</template>

// 服务端预先请求数据，编译后为客户端使用的静态数据
// 当前是查询语句
<page-query>
query ($page: Int) {
  posts: allPost (perPage: 5, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        id
        title
      }
    }
  }
}
</page-query>

<script>

export default {
}
</script>

<style>
.pager .active {
  color: #fff;
  background-color: #007bff;
  border-color: #007bff;
}

.pager .page-link {
  display: inline;
}
</style>
