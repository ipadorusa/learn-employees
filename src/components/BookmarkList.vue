<template>
  <div>
    <h3>BookmarkList</h3>
    <table class="responsive-table">
      <thead>
        <tr>
          <th>Date</th>
          <th>Category</th>
          <th>Title</th>
          <th>Url</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="list in bookmarklist" v-bind:key="list.url">
          <td>{{list.date}}</td>
          <td>{{list.category}}</td>
          <td>{{list.title}}</td>
          <td><a :href="list.url" target="_blank">{{list.url}}</a></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import bookdb from "./firebaseInit";
export default {
  name: 'bookmarklist',
  data() {
    return {
      bookmarklist: [],
    }
  },
  created() {
    bookdb.collection('bookmarklists').orderBy('date').get().then((querySnapshot) =>{
      querySnapshot.forEach((doc) => {
        const bookdata = {
          'category': doc.data().category,
          'date': doc.data().date,
          'title': doc.data().title,
          'url': doc.data().url,
        }
        this.bookmarklist.push(bookdata)
      })
    })
  }
}
</script>

<style>

</style>
