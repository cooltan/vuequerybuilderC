<template>
  <div id="app" class="py-5 px-3">
    <vue-query-builder :rules="rules" v-model="query">
      <template v-slot:default="slotProps">
        <query-builder-group v-bind="slotProps" :query.sync="query"/>
      </template>
    </vue-query-builder>

    <div class="my-6">---</div>

    <p>Generated output:</p>

    <pre>{{ JSON.stringify(this.query, null, 2) }}</pre>
  </div>
</template>

<script>
import VueQueryBuilder from "vue-query-builder";
import QueryBuilderGroup from "./TailwindGroup.vue";

export default {
  name: "App",
  components: {
    VueQueryBuilder,
    QueryBuilderGroup
  },

  data() {
    return {
      rules: [
        {
          type: "text",
          id: "vegetable",
          label: "Vegetable"
        },
        {
          type: "radio",
          id: "fruit",
          label: "Fruit",
          choices: [
            { label: "Apple", value: "apple" },
            { label: "Banana", value: "banana" }
          ]
        }
      ],

      query: {
        logicalOperator: "all",
        children: [
          {
            type: "query-builder-group",
            query: {
              logicalOperator: "any",
              children: [
                {
                  type: "query-builder-rule",
                  query: {
                    rule: "vegetable",
                    operator: "contains",
                    operand: "Vegetable",
                    value: null
                  }
                },
                {
                  type: "query-builder-rule",
                  query: {
                    rule: "fruit",
                    operand: "Fruit",
                    value: "banana"
                  }
                }
              ]
            }
          }
        ]
      }
    };
  }
};
</script>
