<template>
  <div style="width: 100%">
    <draggable class="columns" v-model="BigArray" :option="{group: 'lists'}" @start="drag=true" @end="drag=false">
      <div class="list-elements" v-for="(bigelement,i) in BigArray" :key="bigelement.id">
        <div :style="'background-color: ' + BigArray[i].color">
          <p>{{BigArray[i]['bigname']}}({{BigArray[i]['array'].length}})</p>
          <draggable class="list" v-model="BigArray[i]['array']" :options="{group:'people'}" @start="drag=true" @end="drag=false">
            <div class="card-elements" v-for="element in BigArray[i]['array']" :key="element.id">
              {{element.id}} - {{element.name}}
            </div>
          </draggable>
          <div v-show="!add_new[BigArray[i].id - 1]" class="add-button" @click="addButtonClick(BigArray[i].id - 1)">+ Добавить еще одну карточку</div>
          <div v-show="add_new[BigArray[i].id - 1]">
            <textarea style="width: 90%; height: 10vh;" :ref="'newnamearea' + BigArray[i].id"></textarea>
            <div style="text-align: left">
              <button class="green" @click="addName(BigArray[i].id)">Добавить карточку</button>
              <button class="empty" @click="closeAddName(BigArray[i].id-1)">✕</button>
            </div>
          </div>
        </div>
      </div>
    </draggable>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
export default {
  name: 'MyCards',
  components: {
    draggable
  },
  data () {
    return {
      add_new: [],
      BigArray: [
        {
          'bigname': 'Имена',
          'color': 'red',
          'array': [
            {
              'name': 'Петя',
              'id': 0
            },
            {
              'name': 'Вася',
              'id': 1
            },
            {
              'name': 'Коля',
              'id': 2
            }
          ],
          'id': 1
        },
        {
          'bigname': 'Names',
          'color': 'yellow',
          'array': [
            {
              'name': 'John',
              'id': 0
            },
            {
              'name': 'Joao',
              'id': 1
            },
            {
              'name': 'Jean',
              'id': 2
            }
          ],
          'id': 2
        },
        {
          'bigname': 'Вкусы',
          'color': 'pink',
          'array': [
            {
              'name': 'Горький',
              'id': 0
            },
            {
              'name': 'Соленый',
              'id': 1
            },
            {
              'name': 'Сладкий',
              'id': 2
            }
          ],
          'id': 3
        },
        {
          'bigname': 'Цвета',
          'color': 'blue',
          'array': [
            {
              'name': 'Красный',
              'id': 0
            },
            {
              'name': 'Желтый',
              'id': 1
            },
            {
              'name': 'Розовый',
              'id': 2
            }
          ],
          'id': 4
        }
      ]
    }
  },
  created () {
    this.add_new = new Array(this.BigArray.length).fill(false)
  },
  methods: {
    addButtonClick: function (number) {
      this.add_new.splice(number, 1, true)
    },
    addName: function (number) {
      var newName = this.$refs['newnamearea' + number.toString()][0].value
      var newElement = {}
      newElement.name = newName
      var realNumber = -1
      for (let index = 0; this.BigArray[index].id !== number; index++) {
        realNumber = index
      }
      realNumber += 1
      newElement.id = this.BigArray[realNumber].array.length + 1
      this.BigArray[realNumber].array.push(newElement)
      this.$refs['newnamearea' + number.toString()][0].value = ''
    },
    closeAddName: function (number) {
      this.add_new.splice(number, 1, false)
    }
  }
}
</script>

<style scoped>
.columns {
  cursor: pointer;
  width: 100%;
}
.list-elements {
  width: 20%;
  float: left;
  margin: 1%;
}
.list {
  width: 100%;

}
.card-elements {
  border: 1px solid darkgrey;
  border-radius: 5px;
  background-color: azure;
  margin: 3px;
}
.adder:hover {
  color: red;
}
.textarea {
  width: 100%;
}
.add-button {
  width: border-box;
  // border: 1px solid red;
  text-align: left;
  padding-left: 5%;
}
button.green {
  background-color: #519839;
  box-shadow: 0 1px 0 0 #3f6f21;
  border: none;
  color: #fff;
  padding: 10px;
  margin: 10px;
}
button.green:hover {
  background-color: darkgreen;
}
button.empty {
  background: transparent;
  border: none;
}
button.empty:hover {
  color: black;
}
</style>
