<template>
  <div class="container mt-5">

    <h1 class="text-center">Application de gestion des livres</h1>
    <div class="show">
      <h4>ajouter un livre</h4>
      <button class="btn btn-action" @click="showForm" style="margin:10px ;" >ajouter</button>
    </div>
    <table class="table table-bordered" style="margin-top: 15px;">
      <thead class="thead-dark">
        <tr>
          <th>Id</th>
          <th>Titre</th>
          <th>Auteur</th>
          <th>Prix</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="book in books" :key="book.id">
          <td>{{ book.id }}</td>
          <td>{{ book.title }}</td>
          <td>{{ book.author }}</td>
          <td>{{ book.price }}</td>
          <td>
            <button class="btn btn-action" @click="editBook(book)">Modifer</button>
            <button class="btn btn-action btn-danger" @click="deleteBook(book)">Supprimer</button>
          </td>
        </tr>
      </tbody>
    </table>

    <div class="card" v-if="hidden">
      <div class="card-header">
        <h3 class="text-center">{{ editing ? 'Modifier un livre' : 'Ajouter un livre' }}</h3>
      </div>
      <div class="card-body">
        <form @submit.prevent="saveBook">
          <div class="form-group">
            <label for="title">Titre:</label>
            <input type="text" id="title" class="form-control" v-model="bookForm.title" required>
          </div>
          <div class="form-group">
            <label for="author">Auteur:</label>
            <input type="text" id="author" class="form-control" v-model="bookForm.author" required>
          </div>
          <div class="form-group">
            <label for="author">Prix:</label>
            <input type="text" id="price" class="form-control" v-model="bookForm.price" required>
          </div>
          <button type="submit" class="btn btn-success">{{ editing ? 'Modifier' : 'Ajouter' }}</button>
          <button type="submit" class="btn btn-secondary ml-2" @click="cancelEdit()">Cancel</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      books: [
        { id: 1, title: 'Book 1', author: 'Author 1', price: 100 },
        { id: 2, title: 'Book 2', author: 'Author 2', price: 200 },
      ],
      bookForm: {
        title: '',
        author: '',
        price: 0,
      },
      hidden: false,
      selectedBook: null,
      editing: false,
    };
  },
  methods: {
    showForm() {
      this.hidden = true;
      this.editing = false;
      this.bookForm.title = '';
      this.bookForm.author = '';
      this.bookForm.price = '';
    },
    editBook(book) {
      this.hidden=true;
      this.editing = true;
      this.selectedBook = book;
      this.bookForm.title = book.title;
      this.bookForm.author = book.author;
      this.bookForm.price = book.price;

    },
    deleteBook(book) {

      const id = this.books.indexOf(book);
      if (id !== -1) {
        this.books.splice(id, 1);
      }
      if (this.selectedBook === book) {
        this.selectedBook = null;
      }
    },
    saveBook() {
      if (this.editing) {
        this.selectedBook.title = this.bookForm.title;
        this.selectedBook.author = this.bookForm.author;
        this.selectedBook.price = this.bookForm.price;
      } else {
        const newId = this.books.length + 1;
        const newBook = {
          id: newId,
          title: this.bookForm.title,
          author: this.bookForm.author,
          price: this.bookForm.price
        };
        this.books.push(newBook);
      }

      this.bookForm.title = '';
      this.bookForm.author = '';
      this.bookForm.price = '';
      this.selectedBook = null;
      this.editMode = false;
    },
    cancelEdit() {

      this.editing = false;
      this.bookForm.title = '';
      this.bookForm.author = '';
      this.bookForm.price = '';
      this.selectedBook = null;
    },
    
  },
};
</script>

<style scoped>
/* Custom button style with margins */
.show {
  display: flex;
  
  align-items: center;
}

.btn-action {
  background-color: #919ba4;
  color: #474545;
  margin-right: 5px;
  border-color: #919ba4;
}

.btn-action:hover {
  background-color: #1985f8;
}
</style>
