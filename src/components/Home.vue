<template>
  <v-container>
    <v-layout row wrap>
      <v-flex xs12 text-xs-center>
        <h1>투두 리스트</h1>
        <p>전체 할 일: {{todolist.length}} / 남할 일 :  {{todolist.length - countDone}}/ 완료된 할 일 : {{countDone}}</p>

      </v-flex>

      <v-flex xs6 pa-2>
        <List
        :todolist="todolist"
        @statusControl="statusControl"
        @listDelete="listDelete"
        />
      </v-flex>
      <v-flex xs6 pa-2>
        <listadd
        @listAdd="listAdd"
        @listEdit="listEdit"
        />
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import List from './List'
import Listadd from './Listadd'

export default {
  components: {
    List,
    Listadd
  },
  data() {
    return {
      todolist: []
    }
  },
  computed: {
    countDone(){
      let count = 0
      this.todolist.forEach(list => {
        if (list.status === 'done') count++
      })
      return count
  }
  },
  methods: {
    listAdd(memo) {
      console.log("받았어!")
      this.todolist.push({memo: memo, status: "created"})
    },
    statusControl(index, status){
      this.todolist[index].status=status
    },
    listDelete(index){
      this.todolist.splice(index, 1)
    },
    listEdit(memo, index){
      this.todolist[index].memo = memo
    }
  }
}
</script>
