<template>
  <v-hover>
    <v-card
      slot-scope="{ hover }"
      height="100%"
      :class="`elevation-${hover ? 12 : 2}`"
      class="mx-auto"
    >
      <v-img
        :src="'https://picsum.photos/200/300/?random'"
        height="160"
      ></v-img>
      <v-card-title primary-title>
        <div>
          <div class="headline">{{ data.order }}</div>
          <span class="grey--text">{{ data.catagory }}</span>
          <br />
          <h3>{{ data.type }}</h3>
          Amount: {{ data.amount }} {{ data.unit }}
          <h1>{{ data.price }}/{{ data.unit }}</h1>
        </div>
      </v-card-title>
      <v-card-text>{{ data.description }}</v-card-text>
      <v-spacer />
      <v-card-actions>
        <v-btn flat>Edit</v-btn>
        <v-btn flat @click="remove(data)">Remove</v-btn>
      </v-card-actions>
    </v-card>
  </v-hover>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      default: function() {
        return {};
      }
    },
    remove: {
      type: Function,
      default: function() {
        return;
      }
    }
  }
};
</script>

<style></style>
