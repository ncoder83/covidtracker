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

<h3>Breakdown by Countries ({as_of})</h3>
{#each countries as country}
  <b>Name: {country.Country}</b>
  <br />
  New confirmed: {country.NewConfirmed}
  <br />
  New Recovered: {country.NewRecovered}
  <br />
  New Deaths: {country.NewDeaths}
  <br />
  Total Confirmed: {country.TotalConfirmed}
  <br />
  Total Recovered: {country.TotalRecovered}
  <br />
  Total Deaths: {country.TotalDeaths}
{/each}
