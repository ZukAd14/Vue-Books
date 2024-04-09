<template>
    <div>
        <p>Books amount: {{ books.length }} </p>
        <p>Books price: {{ totalPrice }} </p>
    </div>
</template>

<script>
export default {
  name: 'BooksSummary',
  props: {
    books: {
      type: Array,
      required: true
    }
  },
  computed: {
    totalPrice () {
      return this.books.reduce((total, book) => total + book.price, 0)
    }
  }
}
</script>
