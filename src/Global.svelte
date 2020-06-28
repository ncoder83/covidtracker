<script>
  import Card from "./components/Card.svelte";
  import { onMount } from "svelte";

  let as_of;
  let total_confirmed;
  let new_deaths;
  let total_recovered;
  let new_confirmed;

  onMount(() => {
    var requestOptions = {
      method: "GET",
      redirect: "follow"
    };
    fetch("https://api.covid19api.com/summary", requestOptions)
      .then(response => response.json())
      .then(data => {
        as_of = data.Date;
        total_confirmed = data.Global.TotalConfirmed;
        new_deaths = data.Global.NewDeaths;
        total_recovered = data.Global.TotalRecovered;
        new_confirmed = data.Global.NewConfirmed;
      })
      .catch(error => console.log("error", error));
  });
</script>

<h3>Global({as_of})</h3>
<div class="row">
  <div class="col">
    <Card
      title="Total confirmed"
      text={total_confirmed || 'N/A'}
      textstyle="text-warning" />
  </div>
  <div class="col">
    <Card
      title="New confirmed"
      text={new_confirmed || 'N/A'}
      textstyle="text-warning" />
  </div>
  <div class="col">
    <Card
      title="Total recovered"
      text={total_recovered || 'N/A'}
      textstyle="text-success" />
  </div>
  <div class="col">
    <Card
      title="New death"
      text={new_deaths || 'N/A'}
      textstyle="text-danger" />
  </div>
</div>
