<template>
  <div>
    <div v-if='loading'>Loading...</div>
    <div v-else-if='error'>Error: {{ error.message }}</div>
    <div v-else-if='result && result.languages'>
      {{ result.languages }}
    </div>
  </div>
</template>

<script lang='ts'>
import { defineComponent } from 'vue';
import { useQuery } from '@vue/apollo-composable';
import gql from 'graphql-tag';

export default defineComponent({
  name: 'Languages',
  setup() {
    const { result, loading, error } = useQuery(gql`
      query GetLanguages {
        languages(order_by: {sort: asc, name: asc}) {
          name
          label
        }
      }
    `);
    return { /* your other items, */ result, loading, error };
  }
});
</script>
