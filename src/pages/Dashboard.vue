<template>
  <div class="row">
    <div class="col-12">
      <chart-card
        title="Selection of employee errors per month"
        :chart-data="activityChart.data"
        :chart-options="activityChart.options"
      >
        <span slot="dropdrop">
          <drop-down class="nav-item" title="Errors' name" icon="ti-bell">
            <a class="dropdown-item" href="#">Nhân viên thiếu bảng tên</a>
            <a class="dropdown-item" href="#">Tương tác 1 tay với nhân viên</a>
            <a class="dropdown-item" href="#">Không có nhân viên mở cửa cho khách</a>
            <a class="dropdown-item" href="#">Nhân viên sử dụng điện thoại trong khu vực có KH</a>
          </drop-down>
        </span>
        <span slot="footer">
          <i class="ti-reload"></i> Updated 3 minutes ago
        </span>
        <div slot="legend">
          <i class="fa fa-circle text-info"></i> Nhân viên thiếu bảng tên
        </div>
      </chart-card>
    </div>

    <div class="col-md-6 col-12">
      <chart-card
        title="Today's error"
        :subTitle ="usersChart.today"
        :chart-data="usersChart.data"
        :chart-options="usersChart.options"
      >
        <span slot="footer">
          <i class="ti-reload"></i> Updated 3 minutes ago
        </span>
        <div slot="legend">
          <i class="fa fa-circle text-info"></i> Nhân viên thiếu bảng tên<br />
          <i class="fa fa-circle text-danger"></i> Tương tác 1 tay với nhân viên<br />
          <i class="fa fa-circle text-warning"></i> Không có nhân viên mở cửa cho khách <br />
          <i class="fa fa-circle text-success"></i>Nhân viên sử dụng điện thoại trong khu vực có KH
        </div>
      </chart-card>
    </div>

    <div class="col-md-6 col-12">
      <chart-card
        title="Total Percentage"
        :chart-data="preferencesChart.data"
        chart-type="Pie"
      >
        <span slot="footer">
          <i class="ti-timer"></i> Updated 3 minutes ago
        </span>
        <div slot="legend">
          <i class="fa fa-circle text-info"></i> Nhân viên thiếu bảng tên <br />
          <i class="fa fa-circle text-danger"></i> Không có nhân viên mở cửa cho khách<br />
          <i class="fa fa-circle text-warning"></i> Nhân viên sử dụng điện thoại trong khu vực có KH<br />
        </div>
      </chart-card>
    </div>
  </div>
</template>

<script>
import { StatsCard, ChartCard } from "@/components/index";

export default {
  components: {
    StatsCard,
    ChartCard,
  },
  data() {
    return {
      activityChart: {
        data: {
          labels: [],
          series: [],
        },
        options: {
          seriesBarDistance: 10,
          axisX: {
            showGrid: false,
          },
          height: "245px",
        },
      },
      usersChart: {
        today: new Date().toString(),
        data: {
          labels: [],
          series: [],
        },
        options: {
          seriesBarDistance: 10,
          axisX: {
            showGrid: false,
          },
          height: "245px",
        },
      },
      preferencesChart: {
        data: {
          labels: [],
          series: [],
        },
        options: {},
      },
    };
  },
  mounted() {
    this.loadData();
  },
  methods: {
    async loadData() {
      try {
        const response = await fetch('/data.json');
        const data = await response.json();

        // Process data for each chart
        this.processActivityChart(data);
        this.processUsersChart(data);
        this.processPreferencesChart(data);
      } catch (error) {
        console.error("Error loading data:", error);
      }
    },
    processActivityChart(data) {
    // Group errors by day
    const dailyErrorCount = {};

    data.forEach((item) => {
      const date = item.timestamp.split(" ")[0]; // Extract the date part only

      if (!dailyErrorCount[date]) {
        dailyErrorCount[date] = { "no bills": 0, "one handed interaction": 0, "didn't open door": 0 };
      }

      item.error.forEach((err) => {
        if (dailyErrorCount[date][err] !== undefined) {
          dailyErrorCount[date][err] += 1;
        }
      });
    });

    // Prepare the labels and series data for the chart
    const labels = Object.keys(dailyErrorCount);
    const series = [
      labels.map((date) => dailyErrorCount[date]["no bills"]),
      labels.map((date) => dailyErrorCount[date]["one handed interaction"]),
      labels.map((date) => dailyErrorCount[date]["didn't open door"]),
    ];

    this.activityChart = {
      data: {
        labels,
        series,
      },
      options: {
        seriesBarDistance: 10,
        axisX: {
          showGrid: false,
        },
        height: "245px",
      },
    };
  },
  processUsersChart(data) {
    // Get the current date in the format of the timestamps in the JSON file (YYYY-MM-DD)
    const today = new Date().toISOString().split("T")[0];

    // Filter data for today's entries
    const todayErrors = data.filter(item => item.timestamp.startsWith(today));

    // Initialize the error count for each type
    const errorCount = { "no bills": 0, "one handed interaction": 0, "didn't open door": 0 };

    // Count the occurrences of each error type for today
    todayErrors.forEach(item => {
      item.error.forEach(err => {
        if (errorCount[err] !== undefined) {
          errorCount[err] += 1;
        }
      });
    });

    // Set chart data
      this.usersChart = {
        data: {
          labels: Object.keys(errorCount),
          series: [Object.values(errorCount)],
        },
        options: {
          seriesBarDistance: 10,
          axisX: {
            showGrid: false,
          },
          height: "245px",
        },
      };
    },
    processPreferencesChart(data) {
      const errorCounts = {};

      data.forEach((entry) => {
        entry.error.forEach((errorType) => {
          if (!errorCounts[errorType]) {
            errorCounts[errorType] = 0;
          }
          errorCounts[errorType]++;
        });
      });

      const totalErrors = Object.values(errorCounts).reduce((a, b) => a + b, 0);
      this.preferencesChart.data.labels = Object.keys(errorCounts).map(
        (error) => `${((errorCounts[error] / totalErrors) * 100).toFixed(1)}%`
      );
      this.preferencesChart.data.series = Object.values(errorCounts);
    },
  },
};
</script>
<style></style>
