<template>
  <div
    class="vqb-group relative flex flex-col bg-white rounded border border-gray-300 mb-3"
    :class="'depth-' + depth.toString()"
  >
    <div class="vqb-group-heading rounded-t py-3 px-5 bg-gray-300 border-b border-gray-400">
      <div class="match-type-container form-inline">
        <label class="mr-2" for="vqb-match-type">{{ labels.matchType }}</label>
        
        <select
          id="vqb-match-type"
          v-model="query.logicalOperator"
          class="inline-block w-auto mr-2 h-10 px-1 py-2 leading-normal gray-500 border border-gray-300 rounded"
        >
          <option
            v-for="label in labels.matchTypes"
            :key="label.id"
            :value="label.id"
          >{{ label.label }}</option>
        </select>
        
        <button
          v-if="depth > 1"
          type="button"
          class="close ml-auto"
          @click="remove"
          v-html="labels.removeGroup"
        ></button>
      </div>
    </div>

    <div class="vqb-group-body flex-auto p-5 mb-px">
      <div class="mb-5 flex flex-wrap items-center">
        <div class="form-group flex items-center flex-none">
          <select
            v-model="selectedRule"
            class="inline-block w-auto mr-2 h-10 px-1 py-2 leading-normal gray-500 border border-gray-300 rounded"
          >
            <option v-for="rule in rules" :key="rule.id" :value="rule">{{ rule.label }}</option>
          </select>
          
          <button
            type="button"
            class="text-white px-3 py-2 rounded bg-gray-600 mr-2"
            @click="addRule"
          >{{ labels.addRule }}</button>
          
          <button
            v-if="depth < maxDepth"
            type="button"
            class="text-white px-3 py-2 rounded bg-gray-600"
            @click="addGroup"
          >{{ labels.addGroup }}</button>
        </div>
      </div>

      <query-builder-children v-bind="$props"/>
    </div>
  </div>
</template>

<script>
import QueryBuilderGroup from "vue-query-builder/dist/group/QueryBuilderGroup.umd.js";
import QueryBuilderRule from "./TailwindRule.vue";

export default {
  name: "QueryBuilderGroup",

  components: {
    QueryBuilderRule: QueryBuilderRule
  },

  extends: QueryBuilderGroup
};
</script>

<style>
.vue-query-builder .vqb-group.depth-1 .vqb-rule,
.vue-query-builder .vqb-group.depth-2 {
  border-left: 2px solid #8bc34a;
}

.vue-query-builder .vqb-group.depth-2 .vqb-rule,
.vue-query-builder .vqb-group.depth-3 {
  border-left: 2px solid #00bcd4;
}

.vue-query-builder .vqb-group.depth-3 .vqb-rule,
.vue-query-builder .vqb-group.depth-4 {
  border-left: 2px solid #ff5722;
}

.vue-query-builder .close {
  opacity: 1;
  color: rgb(150, 150, 150);
}

@media (min-width: 768px) {
  .vue-query-builder .vqb-rule.form-inline .form-group {
    display: block;
  }
}
</style>