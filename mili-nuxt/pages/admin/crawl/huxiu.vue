<template>
  <Row>
    <h1 class="crawler-title">虎嗅</h1>
    <crawler
      :from="3"
      :defaultURL="url"
      :cateId="cateId"
      :categories="categories"
    />
  </Row>
</template>

<script>
import crawler from "~/components/admin/crawler";
import request from "~/net/request";

export default {
  asyncData(context) {
    return request
      .getCategories({
        client: context.req,
      })
      .then((res) => {
        let categories = res.data.categories;
        return {
          cateId: (categories && categories[0].id + "") || "",
          categories: categories,
        };
      })
      .catch((err) => {
        console.log(err);
        context.error({ statusCode: 404, message: "Page not found" });
      });
  },

  data() {
    return {
      url: "https://www.huxiu.com",
    };
  },
  components: {
    crawler: crawler,
  },
  head() {
    return {
      title: "抓取虎嗅",
    };
  },
  layout: "admin",
};
</script>

<style>
.crawler-title {
  font-size: 22px;
  margin: 12px 0 12px 0;
}
</style>
