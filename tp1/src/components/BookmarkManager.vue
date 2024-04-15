<template>
    <div>
       <h1>Gestionnaire de Favoris</h1>
       <form @submit.prevent="addBookmark">
         <input v-model="newBookmark.name" placeholder="Nom" required />
         <input v-model="newBookmark.url" placeholder="URL" required />
         <input v-model="newBookmark.categories" placeholder="Catégories" />
         <button type="submit">Ajouter</button>
       </form>
       <br>
       <input v-model="filter" placeholder="Filtrer par catégorie" />
       <ul>
         <li v-for="bookmark in filteredBookmarks" :key="bookmark.id">
           <a :href="bookmark.url" target="_blank">{{ bookmark.name }}</a>
           <span> -> {{ bookmark.categories }}</span>
           <button @click="deleteBookmark(bookmark.id)">Supprimer</button>
         </li>
       </ul>
    </div>
   </template>
   
   <script>
   import { ref, computed } from 'vue';
   
   export default {
    setup() {
       const bookmarks = ref([]);
       const newBookmark = ref({
         id: 0,
         name: '',
         url: '',
         categories: '',
       });
       const filter = ref('');
   
       const addBookmark = () => {
        console.log(newBookmark.value);
        console.log(bookmarks.value);
         newBookmark.value.id = bookmarks.value.length;
         bookmarks.value.push({ ...newBookmark.value });
         newBookmark.value = { id: 0, name: '', url: '', categories: '' };
       };
   
       const deleteBookmark = (id) => {
         bookmarks.value = bookmarks.value.filter(bookmark => bookmark.id !== id);
         console.log(bookmarks.value);
       };
   
       const filteredBookmarks = computed(() => {
         if (!filter.value) return bookmarks.value;
         return bookmarks.value.filter(bookmark => bookmark.categories.includes(filter.value));
       });
   
       return {
         bookmarks,
         newBookmark,
         filter,
         addBookmark,
         deleteBookmark,
         filteredBookmarks,
       };
    },
   };
   </script>