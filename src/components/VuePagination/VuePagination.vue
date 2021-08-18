<template>
  <nav class="pagination is-centered" role="navigation" aria-label="pagination">
    <a
      @click="page -= 1"
      :class="{ 'is-static': !hasPrevPage }"
      class="pagination-previous ml-5 button"
      >Previous</a
    >
    <a
      @click="page += 1"
      :class="{ 'is-static': !hasNextPage }"
      class="pagination-next mr-5 button"
      >Next page</a
    >
    <ul class="pagination-list">
      <li v-show="page === lastPage">
        <a
          @click="page -= 2"
          class="pagination-link"
          :aria-label="'page' + (page - 2)"
          >{{ page - 2 }}</a
        >
      </li>
      <li v-show="page + 1 === lastPage || page === lastPage || page - 1 > 0">
        <a
          @click="page -= 1"
          class="pagination-link"
          :aria-label="'page' + (page - 1)"
          >{{ page - 1 }}</a
        >
      </li>
      <li>
        <a class="pagination-link is-current" :aria-label="'page' + page">{{
          page
        }}</a>
      </li>
      <li v-show="page + 1 <= lastPage">
        <a
          @click="page += 1"
          class="pagination-link"
          :aria-label="'page' + (page + 1)"
          >{{ page + 1 }}</a
        >
      </li>
      <li v-show="page === 1">
        <a
          @click="page += 2"
          class="pagination-link"
          :aria-label="'page' + (page + 2)"
          >{{ page + 2 }}</a
        >
      </li>
    </ul>
  </nav>
  <div class="is-flex is-justify-content-center is-flex-wrap-wrap">
    <div
      v-for="el in filteredList"
      :key="el.title"
      class="card m-2"
      style="max-width: 260px;"
    >
      <div class="card-image">
        <figure class="image is-4by3">
          <img :src="getImgUrl(el.img)" alt="Placeholder image" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-left">
            <figure class="image is-48x48">
              <img
                src="https://bulma.io/images/placeholders/96x96.png"
                alt="Placeholder image"
              />
            </figure>
          </div>
          <div class="media-content">
            <p class="title is-4">{{ el.title }}</p>
            <p class="subtitle is-6">@johnsmith</p>
          </div>
        </div>

        <div class="content">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus nec
          iaculis mauris. <a>@bulmaio</a>. <a href="#">#css</a>
          <a href="#">#responsive</a>
          <br />
          <time datetime="2016-1-1">11:09 PM - 1 Jan 2016</time>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PaginationPage',
  data() {
    return {
      list: [
        { title: 'title 1', img: '1.jpg' },
        { title: 'title 2', img: '2.jpg' },
        { title: 'title 3', img: '3.jpg' },
        { title: 'title 4', img: '4.jpg' },
        { title: 'title 5', img: '5.jpg' },
        { title: 'title 6', img: '6.jpg' },
        { title: 'title 7', img: '7.jpg' },
        { title: 'title 8', img: '8.jpg' },
        { title: 'title 9', img: '9.jpg' },
        { title: 'title 10', img: '10.jpg' },
        { title: 'title 11', img: '11.jpg' },
        { title: 'title 12', img: '12.jpg' },
        { title: 'title 13', img: '13.jpg' },
        { title: 'title 14', img: '14.jpg' },
        { title: 'title 15', img: '15.jpg' },
        { title: 'title 16', img: '16.jpg' },
        { title: 'title 17', img: '17.jpg' },
      ],
      page: 5,
    };
  },
  props: {
    elementsPerPage: {
      type: Number,
      required: true,
    },
  },
  methods: {
    getImgUrl(pic) {
      return require('../assets/' + pic);
    },
  },
  created() {
    const url = new URL(window.location.href);
    const urlPage = url.searchParams.get('page');

    this.page = +urlPage;
  },
  watch: {
    page() {
      window.history.pushState(
        null,
        document.title,
        `${window.location.pathname}?page=${this.page}`
      );
    },
  },
  computed: {
    start() {
      return (this.page - 1) * this.elementsPerPage;
    },
    end() {
      return this.page * this.elementsPerPage - 1;
    },
    filteredList() {
      return this.list.slice(this.start, this.end + 1);
    },
    hasNextPage() {
      return this.end <= this.list.length;
    },
    hasPrevPage() {
      return this.page !== 1;
    },
    lastPage() {
      return Math.ceil(this.list.length / this.elementsPerPage);
    },
    midPage() {
      return Math.ceil(this.lastPage / 2);
    },
  },
};
</script>
