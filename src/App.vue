<template>
  <div id="app" class="container">
    <header class="header">
      <h1>Search</h1>
    </header>

    <div class="search-container">
      <input
          type="text"
          v-model="searchTerm"
          placeholder="Search articles..."
          class="search-input"
      />
    </div>

    <div v-if="searchTerm" class="results-count">
      {{ filteredArticles.length }} posts were found.
    </div>

    <div v-for="article in filteredArticles" :key="article.id" class="article">
      <h2 v-html="highlightText(article.title, searchTerm)" class="article-title"></h2>
      <p class="article-date">{{ article.date }}</p>
      <p v-html="highlightText(article.description, searchTerm)" class="article-description"></p>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      searchTerm: "",
      articles: [
        {
          id: 1,
          title: "My Journey in Software Engineering: From Beginner to Expert",
          description:
              "Over 6 years of experience in developing web and mobile applications using technologies like PHP, Laravel, Vue.js, and AWS. Here's how I evolved in my career.",
          date: "Jan 15, 2018",
        },
        {
          id: 2,
          title: "Building Innovative SaaS Solutions in Germany",
          description:
              "As a software developer aspiring to relocate to Germany, I focus on creating innovative SaaS solutions and enhancing user experiences. Learn about my recent projects.",
          date: "Oct 10, 2023",
        },
        {
          id: 3,
          title: "Mastering Laravel: Best Practices for Scalable Web Applications",
          description:
              "Laravel has been at the core of my development stack. In this article, I share tips and best practices for creating robust and scalable applications.",
          date: "Aug 20, 2024",
        },
      ],
    };
  },
  computed: {
    filteredArticles() {
      return this.articles.filter(
          (article) =>
              article.title.toLowerCase().includes(this.searchTerm.toLowerCase()) ||
              article.description
                  .toLowerCase()
                  .includes(this.searchTerm.toLowerCase())
      );
    },
  },
  methods: {
    highlightText(text, query) {
      if (!query) return text;
      const regex = new RegExp(`(${query})`, "gi");
      return text.replace(regex, `<span class="highlight">$1</span>`);
    },
  },
};
</script>

<style>
.container {
  font-family: 'Arial', sans-serif;
  padding: 20px;
  max-width: 800px;
  margin: 0 auto;
  color: #333;
  line-height: 1.6;
}

.header h1 {
  font-size: 2rem;
  margin-bottom: 20px;
}

.search-container {
  margin-bottom: 20px;
}

.search-input {
  width: 100%;
  padding: 12px 16px;
  border: 1px solid #ddd;
  border-radius: 6px;
  font-size: 1rem;
}

.results-count {
  font-size: 1.1rem;
  margin-bottom: 20px;
  font-weight: bold;
}

.article {
  padding: 15px 0;
  border-bottom: 1px solid #eee;
}

.article-title {
  font-size: 1.4rem;
  font-weight: bold;
  margin: 0;
  color: #333;
}

.article-date {
  font-size: 0.9rem;
  color: #aaa;
  margin: 5px 0;
}

.article-description {
  font-size: 1rem;
  color: #555;
  margin: 0;
}

.highlight {
  background-color: yellow;
  font-weight: bold;
}

</style>
