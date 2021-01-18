<template>
  <input type="text" placeholder="search by book title" v-model="input" />
  <div class="all-books">
    <div v-for="book in filterBook" :key="book.id" class="book">
      <img :src="book.url" />
      <span class="book-title">Title: {{ book.title }}</span>
      <span>Author: {{ book.author }}</span>
      <span class="price"> Price: ₹{{ book.price }}</span>
    </div>
  </div>
</template>

<script>
import { computed, reactive, ref } from "vue";
export default {
  props: ["books"],
  setup(props) {
    const input = ref("");
    function capitalizeFirstLetter(string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    }

    const filterBook = computed(() => {
      return props.books.filter((book) => {
        return book.title.includes(capitalizeFirstLetter(input.value));
      });
    });

    return { input, filterBook };
  },
};
</script>

<style>
img {
  width: 200px;
}
.book {
  background-color: white;
  margin: 20px auto;
  width: 350px;
  border-radius: 10px;
  padding: 10px;
  box-shadow: 3px 3px rgb(122, 250, 244);
}
.all-books {
  display: grid;
  grid-template-columns: auto auto auto;
  grid-gap: 20px;
}
input {
  border: none;
  background: none;
  border: 2px solid black;
  background: rgb(122, 250, 244);
  border-radius: 10px;
  padding: 10px;
  color: white;
  font-size: 20px;
}
span {
  display: block;
  color: rgb(216, 97, 0);
  text-transform: capitalize;
  letter-spacing: 1px;
}
.price {
  color: green;
}
.book-title {
  color: blueviolet;
}

@media screen and (max-width: 850px) {
  .all-books {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
  }
}
@media screen and (max-width: 500px) {
  .all-books {
    display: block;
  }
}
</style>