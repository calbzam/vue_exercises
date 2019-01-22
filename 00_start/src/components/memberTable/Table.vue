<template>
  <div>
    <h2>Member Page</h2>
    <p>Company name: {{ company }}</p>
    <input v-model="company"  @change="changeCompany(company)"placeholder="Company name">
    <button @click="loadMembers(company)">Load</button>
    <table :class="$style.table">
      <thead>
        <member-head/>
      </thead>
      <tbody>
        <template v-for="member in members">
          <member-row :key="member.id" :member="member"/>
        </template>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import MemberHead from "./Head.vue";
import MemberRow from "./Row.vue";
import { Member } from "../../model/member";
import { getAllMembers } from "../../api/memberAPI";

export default Vue.extend({
  name: "MemberTable",
  components: { MemberHead, MemberRow },
  data: () => ({
    members: [] as Member[],
    company: "lemoncode"
  }),
  methods: {
    loadMembers: function(company) {
      getAllMembers(company).then(members => {
        this.members = members;
      });
    },
    changeCompany: function(company) {
        this.company = company;
      }
  }
});
</script>

<style module>
.table {
  border-collapse: collapse;
  width: 100%;
}

.table tbody tr:nth-of-type(odd) {
  background-color: rgba(0, 0, 0, 0.05);
}
</style>
