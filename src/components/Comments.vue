<template>
  <div class="container">
    <h1>Comentarios</h1>
    <hr />
    <FormTodo v-on:add-todo="addComment"></FormTodo>
    <div class="list-group" style="margin-top: 10px;">
      <p v-if="comments.length <= 0">Sem comentários...</p>
      <div class="list-group-item" v-for="(comment, index) in allComments" :key="comment.id">
        <span class="comment_author">
          Autor: <strong>{{ comment.name }}</strong>
        </span>
        <p> {{ comment.message }}</p>
        <div>
          <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)">Excluir</a>
        </div>
      </div>
    </div>
    <hr/>
  </div>
</template>

<script>

import FormTodo from './FormTodo';

export default {
  //para ulilizar um outro componente é necessario
  //importar o componente 
  components: {
    FormTodo,
  },
  //disponibiliza variaveis
  data(){
    return {
      comments: [],
      }
    },
  //metodos do componente
  methods: {
    addComment(comments){
      this.comments.push(comments);
    },
    removeComment(index){
      console.log(index);
      this.comments.splice(index, 1);
    }
  },
  //tambem disponibiliza variaveis
  computed: {
    allComments(){
      return this.comments.map(comment => ({
        ...comment,
        name: comment.name.trim() === '' ? 'Anônimo': comment.name
      }))
    }
  },
  //identifica quando a variavel recebe alguma alteração
  watch: {
    comments(val) {
      console.log('val',val)
    }
  }
}
</script>

