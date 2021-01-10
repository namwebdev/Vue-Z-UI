<template>
  <div id="app">
    <vue-cascader-select
      :options="getTeams"
      @select="(selected) => (value = selected.value)"
      @clear="() => (value = '')"
      :value="value"
    />
  </div>
</template>

<script>
import VueCascaderSelect from "./components/CascaderSelect";

export default {
  name: "App",
  components: {
    VueCascaderSelect,
  },
  data() {
    return {
      value: "",
    };
  },
  computed: {
    getTeams() {
      return [
        {
          label: "Eastern Conference",
          value: "Eastern Conference",
          disabled: true,
          options: [
            {
              label: "Southeast",
              value: "Southeast",
              options: [
                {
                  label: "Atlanta Hawks",
                  value: "Atlanta Hawks",
                  options: [
                    { label: "Trae Young", value: "Trae Young" },
                    { label: "Clint Capela", value: "Clint Capela" },
                  ],
                },
                { label: "Charlotte Hornets", value: "Charlotte Hornets" },
                { label: "Miami Heat", value: "Miami Heat" },
                { label: "Orlando Magic", value: "Orlando Magic" },
                { label: "Washington Wizards", value: "Washington Wizards" },
              ],
            },
            {
              label: "Atlantic",
              value: "Atlantic",
              options: [
                { label: "Boston Celtics", value: "Boston Celtics" },
                { label: "Brooklyn Nets", value: "Brooklyn Nets" },
                { label: "New York Knicks", value: "New York Knicks" },
                { label: "Philadelphia 76ers", value: "Philadelphia 76ers" },
                { label: "Toronto Raptors", value: "Toronto Raptors" },
              ],
            },
            {
              label: "Central",
              value: "Central",
              options: [
                { label: "Chicago Bulls", value: "Chicago Bulls" },
                { label: "Cleveland Cavaliers", value: "Cleveland Cavaliers" },
                { label: "Detroit Pistons", value: "Detroit Pistons" },
                { label: "Indiana Pacers", value: "Indiana Pacers" },
                { label: "Milwaukee Bucks", value: "Milwaukee Bucks" },
              ],
            },
          ],
        },
        {
          label: "Western Conference",
          value: "Western Conference",
          disabled: true,
          options: [
            {
              label: "Southwest",
              value: "Southwest",
              options: [
                { label: "Dallas Mavericks", value: "Dallas Mavericks" },
                { label: "Houston Rockets", value: "Houston Rockets" },
                { label: "Memphis Grizzlies", value: "Memphis Grizzlies" },
                {
                  label: "New Orleans Pelicans",
                  value: "New Orleans Pelicans",
                },
                { label: "San Antonio Spurs", value: "San Antonio Spurs" },
              ],
            },
            {
              label: "Northwest",
              value: "Northwest",
              options: [
                { label: "Denver Nuggets", value: "Denver Nuggets" },
                {
                  label: "Minnesota Timberwolves",
                  value: "Minnesota Timberwolves",
                },
                {
                  label: "Oklahoma City Thunder",
                  value: "Oklahoma City Thunder",
                },
                {
                  label: "Portland Trail Blazers",
                  value: "Portland Trail Blazers",
                },
                { label: "Utah Jazz", value: "Utah Jazz" },
              ],
            },
            {
              label: "Pacific",
              value: "Pacific",
              options: [
                {
                  label: "Golden State Warriors",
                  value: "Golden State Warriors",
                },
                {
                  label: "Los Angeles Clippers",
                  value: "Los Angeles Clippers",
                },
                { label: "Los Angeles Lakers", value: "Los Angeles Lakers" },
                { label: "Phoenix Suns", value: "Phoenix Suns" },
                { label: "Sacramento Kings", value: "Sacramento Kings" },
              ],
            },
          ],
        },
      ];
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
