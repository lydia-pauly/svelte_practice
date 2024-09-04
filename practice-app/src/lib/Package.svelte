<script>
  export let name;
  export let version;
  export let speed;
  export let website;

  $: href = `https://www.npmjs.com/package/${name}`
</script>

<p>
  The <code>{name}</code> package is {speed} fast and you can download version {version} from
  <a href={href}>npm</a> and <a href={website}>learn more here</a>
</p>
