<template>
  <div class="form">
    <v-form>
      <v-container>
        <v-layout>
          <v-flex xs12 md4>
            <header>Stack</header>
          </v-flex>
        </v-layout>
        <v-layout>
          <v-flex xs6 md4>
            <v-text-field
              v-model="item.value"
              :counter="40"
              label="Value"
              required
            ></v-text-field>
          </v-flex>
        </v-layout>
        <v-layout v-for="item in stack" :key="item.id">
          <v-flex xs6 md4>
            <v-text-field label="Value" v-model="item.value"></v-text-field>
          </v-flex>
          <v-flex xs4 md4>
            <v-btn color="#42f48c" @click='removeItem(item.id)'>X</v-btn>
          </v-flex>
        </v-layout>

        <v-layout>
          <v-flex xs12 md4>
            <v-btn color="#42f48c" @click='addItem(item.value)'>Add Item</v-btn>
          </v-flex>
        </v-layout>
      </v-container>
    </v-form>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import {Item} from '../services/Item';

export default Vue.extend({
    name: 'Form',
    created: function() {
        this.updateStack();
    },
    props: {
        stack: {
            type: Array,
            default: () => [],
        },
    },
    data: () => ({
        item: {
            id: 1,
            value: '',
        }
    }),
    methods: {
        addItem(value) {
            this.$http.post('https://localhost:44349/api/stack', value)
        },
        removeItem(id: number) {
            
        },
        updateStack() {
            this.$http.get(
              'https://localhost:44349/api/stack'
            ).then((response) => {
                this.$props.stack = response.data;
            });
        },
    },
});
</script>
