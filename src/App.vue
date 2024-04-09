
<template>
  <div id="app">

    <!-- heading -->
    <header>
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
    books: [
      {
        title: 'The Catcher in the Rye',
        price: 20
      },
      {
        title: 'Of Mice and Men',
        price: 18
      }
    ]
  }),
  methods: {
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
