<script>
  import { onMount } from "svelte";

  // https://covidtracking.com/api/states/info
  let states = [];
  let state_filter = "";

  $: filtered_result = state_filter
    ? states.filter(s => {
        return s.state.toLowerCase().startsWith(state_filter.toLowerCase());
      })
    : states;

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

  function getStyleForQuality(input) {
    switch (input) {
      case "A+":
      case "A":
      case "A-":
        return "text-success";
      case "B+":
      case "B":
      case "B-":
        return "text-info";
      case "C+":
      case "C":
      case "C-":
        return "text-warning";
      case "D+":
      case "D":
      case "D-":
        return "text-danger";
      default:
        return "text-danger";
    }
  }
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
<h3>US States</h3>
<input
  type="text"
  class="form-control"
  placeholder="Filter states"
  bind:value={state_filter} />
{#each filtered_result as state}
  <h4>
    {state.state} ({state.dateChecked})
    <span class="float-right badge badge-pill badge-primary">
      {state.dataQualityGrade}
    </span>
    <span class="float-right text-info">data quality:</span>
  </h4>

  <div class="table-responsive">
    <table class="table table-bordered">
      <thead class="thead-dark">
        <tr>
          <th>Cases</th>
          <th>Tests negative</th>
          <th>Tests pending</th>
          <th>Hospitalized currently</th>
          <th>Hospitalized cumulative</th>
          <th>In ICU currently</th>
          <th>In ICU cumulative</th>
          <th>On Ventilator currently</th>
          <th>Recovered</th>
          <th>Deaths</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>{state.positive || 'N/A'}</td>
          <td>{state.negative || 'N/A'}</td>
          <td>{state.pending || 'N/A'}</td>
          <td>{state.hospitalizedCurrently || 'N/A'}</td>
          <td>{state.hospitalizedCumulative || 'N/A'}</td>
          <td>{state.inIcuCurrently || 'N/A'}</td>
          <td>{state.inIcuCumulative || 'N/A'}</td>
          <td>{state.onVentilatorCurrently || 'N/A'}</td>
          <td>{state.recovered || 'N/A'}</td>
          <td>{state.death || 'N/A'}</td>
        </tr>
      </tbody>
    </table>
  </div>
{/each}
