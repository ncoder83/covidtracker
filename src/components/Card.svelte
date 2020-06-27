<script>
  export let text;
  export let title;
  export let textstyle = "text-muted";

  import { Card, CardBody, CardSubtitle, CardText } from "sveltestrap";
</script>

<Card class="mb-3">
  <CardBody>
    <CardSubtitle>
      <b>{title}</b>
    </CardSubtitle>
    <CardText class={textstyle}>
      <b>{text}</b>
    </CardText>
  </CardBody>
</Card>
