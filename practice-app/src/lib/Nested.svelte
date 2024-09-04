<script>
// This is a child component for app.svelte or a +page.svelte
// Quite often, you will need to be passed data from the parent
// In order to inherit a "prop" (SH for property), then you will need to export the variable with an assingment, like so:
export let answer="Default me";
// Note how you can also define a default value - useful for error catching
</script>

<p>This is the Nested component</p>
<p>This is the answer: {answer}</p>

<style>
  p {
    color: goldenrod;
  }
</style>
