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
          <v-flex xs8 md4>
            <v-text-field
              v-model="item.value"
              :counter="40"
              label="Value"
              required
            ></v-text-field>
          </v-flex>
          <v-flex xs1 md4>
            <v-btn color="#42f48c" @click='addItem(item.value).then(() => updateStack());'>+</v-btn>
          </v-flex>
        </v-layout>
        <v-layout v-for="item in stack.slice().reverse()" :key="item.id">
          <v-flex xs6 md4>
            <v-text-field label="Value" v-model="item.value" readonly></v-text-field>
          </v-flex>
          <v-flex xs4 md4 v-if="item.id == stack.length - 1">
            <v-btn color="#42f48c" @click='removeItem().then(() => updateStack());'>X</v-btn>
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
    created() {
        this.updateStack();
    },
    data: () => ({
        item: {
            id: 1,
            value: '',
        },
        stack: [],
    }),
    methods: {
        addItem(value: string) {
            return this.$http.post('https://localhost:44349/api/stack/', {id: '0', value});
        },
        updateStack() {
            this.$http.get(
              'https://localhost:44349/api/stack',
            ).then((response) => {
                this.$data.stack = response.data;
            });
        },
        removeItem() {
            return this.$http.delete('https://localhost:44349/api/stack/');
        },
    },
});
</script>
