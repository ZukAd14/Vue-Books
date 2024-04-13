
<template>
  <div id="app" class="app">

    <!-- heading -->
    <header class="app__heading">
      <h1>Books<span>.app</span></h1>
    </header>

    <!-- books list -->
    <books-list
      @remove="removeBook"
      :books="books" />

    <BooksLengthMsg
      :booksAmount="books.length"
    />

    <!-- add book form -->
    <book-form
      @add="addBook" />

      <BooksSummary
      :books="books" />
  </div>
</template>

<script>
import BooksList from './components/BooksList'
import BooksLengthMsg from './components/BooksLengthMsg.vue'
import BookForm from './components/BookForm.vue'
import BooksSummary from './components/BooksSummary.vue'

export default {
  name: 'App',
  data: () => ({
    books: []
  }),
  created () {
    this.fetchBooks()
  },
  methods: {
    async fetchBooks () {
      try {
        const response = await fetch('https://api.itbook.store/1.0/new')
        const data = await response.json()
        this.books = data.books.slice(0, 3).map(book => ({
          title: book.title,
          price: book.price
        }))
      } catch (error) {
        console.error('Error fetching books: ', error)
      }
    },
    removeBook (index) {
      this.books.splice(index, 1)
    },
    addBook (book) {
      this.books.push({ ...book })
    }
  },
  components: {
    BooksList,
    BooksLengthMsg,
    BookForm,
    BooksSummary
  }
}
</script>

<style lang="scss">
.app {
  width: 100%;
  max-width: 1000px;
  padding: 2rem;
  margin: 0 auto;

  &__heading {
    font-size: 3rem;
    text-align: center;
    span {
      color: #5a58da;
    }
  }
}
</style>
