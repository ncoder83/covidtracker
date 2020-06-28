<script>
  import { onMount } from "svelte";

  // https://covidtracking.com/api/states/info
  export var bookmark;
  let states = [];
  let state_filter = bookmark || "";

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
