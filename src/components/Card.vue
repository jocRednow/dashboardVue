<template>
  <div class="col-md-4">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">{{ title }}</h5>
      </div>
      <draggable class="dragArea list-group list-group-flush"
        :list="list"
        group="people" @change="log">
        <div
          @dblclick="removeCard(i)"
          title="Double click will delete card"
          class="list-group-item"
          v-for="(element, i) in list"
          :key="i">
          {{ element.text }}
        </div>
      </draggable>
      <div class="card-body">
        <form class="input-group" @submit.prevent="addNewCard">
            <div class="input-group-prepend">
              <button class="btn btn-outline-secondary btn-sm" type="button" id="add-button" 
                @click="toggleAddNew">{{ toggle === false ? 'Add' : 'Clear' }}</button>
            </div>
            <input v-if="toggle" type="text" class="form-control form-control-sm" v-model="newCard.text"
            placeholder="Set new card" aria-label="add button" aria-describedby="add-button">
        </form>
      </div>
    </div>
  </div> 
</template>

<script>
import draggable from 'vuedraggable';

export default {
  name: 'Card',
  props: ['title', 'list', 'onRemoveCard'],
  data () {
    return {
      toggle: false,
      newCard: { text: '' }
    }
  },
  components: {
    draggable
  },
  methods: {
    toggleAddNew () {
      this.toggle = !this.toggle;
      if (this.toggle === false) this.newCard = { text: '' };
    },
    addNewCard () {
      if (this.newCard.text.length > 0) {
        this.list.push(this.newCard);
        this.toggleAddNew();
      } else return false;
    },
    // Подумал, что нехватает кнопки "Удалить"
    removeCard (index) {
      // Можно было бы и через store всё это прокинуть, тем более, что я привычно поставил ещё и Vuex. 
      // Но так быстрее :)
      this.$emit('onRemoveCard', {
        index: index,
        title: this.title
      })
    },
    log (evt) {
      console.log(evt);
    }
  }
}
</script>

<style scoped>
  .card-body {
    text-align: center;
    background-color: #f2f2f2;
  }
  .list-group-item {
    cursor: pointer;
    margin: 0 5% 1% 5%;
  }
</style>
