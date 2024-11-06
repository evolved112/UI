<template>
  <div class="row">
    <div class="col-12">
      <card :title="table1.title" :subTitle="table1.subTitle">
        <div slot="raw-content" class="table-responsive">
          <paper-table :data="table1.data" :columns="table1.columns">
          </paper-table>
        </div>
      </card>
    </div>
  </div>
</template>

<script>
import { PaperTable } from "@/components";
const tableColumns = [ "Timestamp", "Identity", "Error"];

export default {
  components: {
    PaperTable,
  },
  data() {
    return {
      table1: {
        title: "Errors Report",
        columns: [...tableColumns],
        data: [], // initialize as empty
      },
    };
  },
  mounted() {
    this.loadData();
  },
  methods: {
    async loadData() {
      try {
        const response = await fetch('/dataNew.json');
        const data = await response.json();
        // Filter out entries with a null error and map them to the table data format
        this.table1.data = data
          .filter(item => item.error !== "null")
          .map(item => ({
            video: item.video,
            timestamp: item.timestamp,
            identity: item.identity,
            error: item.error,
          }));
        console.log(this.table1.data);
      } catch (error) {
        console.error("Error loading data:", error);
      }
    }
  }
};
</script>

<style></style>
