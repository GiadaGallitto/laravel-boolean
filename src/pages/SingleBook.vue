<script>
import axios from 'axios';

export default {
  name: 'SingleBook',
  data() {
    return {
      book: '',
      urlAddress: 'http://127.0.0.1:8000',
    }
  },
  methods: {
    getBook() {
      axios.get(this.urlAddress + `/api/books/${this.$route.params.id}`, {
        params: {

        }
      })
        .then((response) => {
          console.log(response.data.results)
          this.book = response.data.results;
        })
        .catch(function (error) {
          console.log(error);
        });
    },

  },
  created() {
    this.getBook()
  },
}
</script>

<template>
  <section>
    <div class="container">
      <div class="row">
        <div class="col-12">
          <h1>
            {{ book.title }}
          </h1>
        </div>
      </div>
      <div class="row d-flex justify-content-center">
        <div class="col-12 mb-4">
          <div class="card">
            <div class="card-header">{{ book.author.first_name }} {{ book.author.last_name }}  / {{ book.publication_date }} ({{ book.price }}&euro;)</div>
            <img class="card-img-top" :src="book.cover_image" :alt="book.title">
            <div class="card-body">
              <h5 class="card-title">{{ book.title }}</h5>
              <p class="card-text">{{ book.description }}</p>

            </div>
            <div class="card-footer">
              Editor: {{ book.editor }} - - - <span v-for="genre in book.genres">#{{ genre.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss"></style>