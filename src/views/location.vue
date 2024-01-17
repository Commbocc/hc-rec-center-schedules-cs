<template>
  <div v-if="programs.loading" class="text-center my-5">
    <div class="spinner-border" role="status">
      <span class="visually-hidden">Loading...</span>
    </div>
  </div>

  <div v-else-if="programs.data.length" class="accordion accordion-flush">
    <Group
      v-for="(activities, groupName, index) in groupedPrograms"
      :key="index"
      :name="groupName"
      :index="index"
    >
      <Activity
        v-for="{ id, fields } in activities"
        :key="id"
        :fields="fields"
      />
    </Group>
  </div>

  <div v-else class="alert alert-info" role="alert">
    There are no programs at this time.
  </div>
</template>

<script>
import { programs, fetchPrograms, groupedPrograms } from "../lib/programs";
import Group from "../components/Group.vue";
import Activity from "../components/Activity.vue";

export default {
  props: {
    UID: String,
  },

  components: { Group, Activity },

  setup(props) {
    fetchPrograms(props.UID);

    return { programs, groupedPrograms };
  },
};
</script>
