<template>
  <div class="app">
    <div class="container">
      <header-list
        @showDialog='showDialog'
      />
      <form-search
          @formSerchQuery='formSerchQuery'
          @sortFilter='selectedSort'
      />
      <content-list
        class="content_block"
        @btnPost='btnPost'
        @removePost='removePost'
        :sortPost='sortPost'
      />
      <form-dialog
        v-model:show='dialogVisible'
      >
        <form-input
          @closeForm='closeForm'
          @createPost='createPost'
        />
      </form-dialog>
    </div>
  </div>
</template>

<script>
import ContentList from './components/ContentList.vue'
import FormInput from './components/FormInput.vue'
import HeaderList from './components/HeaderList.vue'
import FormDialog from './components/UI/FormDialog.vue'
import FormSearch from './components/UI/FormSearch.vue'

  export default {
    components: { 
      ContentList, 
      FormDialog, 
      FormInput, 
      HeaderList, 
      FormSearch 
    },
    data(){
      return {
        posts: [],
        formDialog: false,
        dialogVisible: false,
        serchQuery: null,
      }
    },
    methods: {
      btnPost(post){
        post.ready = !post.ready;
        if(post.ready === true){
          post.readyText = 'Выполнено';
        } else {
          post.readyText = 'В работе';
        }
      },
      showDialog(){
        this.dialogVisible = true;
      },
      createPost(post){
        this.posts.push(post);
      },
      selectedSort(event){
        if(event === 'Дата -'){
          this.posts.sort((a,b) => new Date(a.date) - new Date(b.date));
        }
        if(event === 'Дата +'){
          this.posts.sort((a,b) => new Date(a.date) - new Date(b.date));
          this.posts.reverse();
        }
        if(event === 'Выполнено'){
          this.posts.sort((a,b) => b.ready - a.ready);
        }
        if(event === 'В работе'){
          this.posts.sort((a,b) => a.ready - b.ready);
        }
      },
      closeForm(){
        this.dialogVisible = false;
      },
      formSerchQuery(value){
        this.serchQuery = value;
      },
      removePost(post){
        this.posts = this.posts.filter(p => p.id !== post.id)
      }
    },
    computed: {
      sortPost(){
        if(this.serchQuery){
          return this.posts.filter(item => {
            return this.serchQuery
              .toLowerCase()
              .split(" ")
              .every(v => item.readyText.toLowerCase().includes(v) ||
                item.title.toLowerCase().includes(v) ||
                item.showDate.toLowerCase().includes(v)
              )
          });
        } else {
          return this.posts;
        }
      }
    },
    mounted() {
      if(localStorage.posts){
        this.posts = JSON.parse(localStorage.posts);
      }
    },
    watch: {
      posts: {
        handler(newValue) {
          localStorage.posts = JSON.stringify(newValue);
        },
        deep: true
      }
    }
  }
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

:active, :hover, :focus {
    outline: 0;
    outline-offset: 0;
}

.app {
  margin-top: 104px;
}

h1 {
  font-family: Montserrat;
  font-weight: 700;
  font-size: 24px;
}

.container {
  max-width: 1300px;
  margin: auto;
}

@media (max-width: 700px) { 
  .container {
    width: 700px;
  }
}

.content_block {
  margin-top: 20px;
}

.add_task {
  width: 40px;
  height: 40px;
  background-color: #D6DBEB;
  border-radius: 20px;
}

@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@700&display=swap')
</style>