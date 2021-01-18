<template>
  <h1 class="heading">Book Show Room</h1>
  <Books :books="books" />
  
</template>

<script>
import { ref } from "vue";
import Books from "../components/Books";

export default {
  components: {
    Books,
  },
  setup() {
    const books = ref([]);
    const error = ref(null);

    const getBooks = async () => {
      try {
        const response = await fetch("http://localhost:3000/books");
        if (!response.ok) {
          throw new Error("SomeThing went Wrong");
        }
        const data = await response.json();
        books.value = data;
      } catch (err) {
        error.value = err.message;
      }
    };
    getBooks();
    return { books, error };
  },
};
</script>

<style >
.heading{
  color: rgb(122, 250, 244)
}
</style>