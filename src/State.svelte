<script>
  import { onMount } from "svelte";

  let states = [];

  onMount(() => {
    var requestOptions = {
      method: "GET",
      redirect: "follow"
    };

    fetch("https://covidtracking.com/api/states", requestOptions)
      .then(response => response.json())
      .then(data => {
        states = data;
        console.log(states);
      });
  });
</script>
 <!-- checkTimeEt: "06/25 20:00"
commercialScore: 0
dataQualityGrade: "A"
date: 20200626
dateChecked: "2020-06-26T00:00:00Z"
dateModified: "2020-06-26T00:00:00Z"
death: 14
deathIncrease: 2
fips: "02"
grade: ""
hash: "2d488ae6053360ee51e30da54826ae89e3d5f6bc"
hospitalized: null
hospitalizedCumulative: null
hospitalizedCurrently: 12
hospitalizedIncrease: 0
inIcuCumulative: null
inIcuCurrently: null
lastUpdateEt: "6/26/2020 00:00"
negative: 100956
negativeIncrease: 2320
negativeRegularScore: 0
negativeScore: 0
negativeTestsViral: null
onVentilatorCumulative: null
onVentilatorCurrently: 2
pending: null
posNeg: 101792
positive: 836
positiveCasesViral: null
positiveIncrease: 20
positiveScore: 0
positiveTestsViral: null
recovered: 519
score: 0
state: "AK"
total: 101792
totalTestResults: 101792
totalTestResultsIncrease: 2340
totalTestsViral: 101792 -->
<h3>Breakdown by States</h3>
{#each states as state}
  <b>Name:</b>
{/each}
