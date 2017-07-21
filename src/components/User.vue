<template>
    <div class="user">
        <ul class="list-group">
            <li class="list-group-item" v-for="item in items">{{ item.name }}</li>
        </ul>
        <pagination :pagination="pagination" :callback="loadData" :options="paginationOptions"></pagination>
    </div>
</template>

<script>
  import axios from 'axios'
  import pagination from 'vue-bootstrap-pagination'

  export default {
    name: 'user',
    data () {
      return {
        items: [],
        pagination: {
          per_page: 0,
          current_page: 1,
          last_page: 0
        },
        paginationOptions: {}
      }
    },
    created () {
      this.loadData()
    },
    methods: {
      loadData () {
        axios.get('http://s-pagination.zone/users/' + this.pagination.current_page)
          .then(response => {
            this.pagination = response.data.pagination
            this.items = response.data.items
          })
          .catch(e => {
            console.log(e)
          })
      }
    },
    components: {
      pagination
    }
  }
</script>