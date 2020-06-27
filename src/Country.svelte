<script>
  import { onMount } from "svelte";

  let countries = [];
  let as_of;

  onMount(() => {
    var requestOptions = {
      method: "GET",
      redirect: "follow"
    };

    fetch("https://api.covid19api.com/summary", requestOptions)
      .then(response => response.json())
      .then(data => {
        as_of = data.Date;
        countries = data.Countries;
      })
      .catch(error => console.log("error", error));
  });
</script>

<h3 class="display-4">Countries ({as_of})</h3>

<input type="text" class="form-control" placeholder="Filter countries" />
{#each countries as country}
  <ul class="list-unstyled">
    <li>
      <b>Name: {country.Country}</b>
      <ul>
        <li>
          New confirmed:
          <span class="text-warning">{country.NewConfirmed}</span>
        </li>
        <li>
          Total Confirmed:
          <span class="text-warning">{country.TotalConfirmed}</span>
        </li>
        <li>
          New Recovered:
          <span class="text-success">{country.NewRecovered}</span>
        </li>
        <li>
          Total Recovered:
          <span class="text-success">{country.TotalRecovered}</span>
        </li>
        <li>
          New Deaths:
          <span class="text-danger">{country.NewDeaths}</span>
        </li>
        <li>
          Total Deaths:
          <span class="text-danger">{country.TotalDeaths}</span>
        </li>
      </ul>
    </li>
  </ul>
{/each}
