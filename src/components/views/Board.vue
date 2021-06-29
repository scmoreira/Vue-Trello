<template>
  <div >
    <h3><span>My panels</span> ▸ {{ name }} </h3>
    <input
      type="text"
      placeholder="Add a list"
      v-model="listName"
      @keyup.enter="add"
    />
    <div class="tasks-collection">
      <span v-if="fetchingData">Loading...</span>
      <Column
        v-for="list in boardList"
        :key="list.id"
        :listId="list.id"
        :name="list.name"
      />
    </div>
  </div>
</template>

<script>
import { mapState, mapActions, mapGetters } from 'vuex'
import Column from '@/components/Column.vue'

export default {
  components: { Column },
  props: {
    name: String,
    id: String
  },
  data () {
    return {
      listName: ''
    }
  },
  computed: {
    ...mapState([
      'lists',
      'fetchingData',
      'error'
    ]),
    ...mapGetters([
      'getListsByBoard'
    ]),
    boardList () {
      return this.getListsByBoard(this.id)
    }
  },
  methods: {
    ...mapActions([
      'fetchLists',
      'addColumn'
    ]),
    add () {
      this.addColumn({ board: this.id, name: this.listName })
      this.listName = ''
    }
  },
  created () {
    this.fetchLists({ board: this.id })
  }
}
</script>

<style lang="scss" scoped>
  .tasks-collection {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    padding-top: 1rem;
  }
  h3 {
    color: #37474f;
    text-align: left;
    margin: 1.5rem;
    span {
      color: #546e7a;
    }
  }
  input {
    background-color: #607d8b;
    border: 0;
    border-radius: 3px;
    box-shadow: 0 0 0 0.5px rgba(49,49,93,.03),
      0 2px 5px 0 rgba(49,49,93,.1),
      0 1px 2px 0 rgba(0,0,0,.08);
    text-align: center;
    color: #607d8b;
    font-size: 1.2rem;
    outline: 0;
    padding: 1rem;
    transition: all 600ms ease;
    &:active,
    &:focus {
      background-color: #fafafa;
    }
    &::placeholder {
      color: #fafafa;
    }
  }
</style>
