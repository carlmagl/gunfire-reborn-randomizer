<script>
  export let weapon;
</script>

<main>
  <div class="weapon">
    <h4>{weapon.name}</h4>
    <img src={weapon.imgUrl} alt={weapon.name} />
  </div>
</main>

<style>
  .weapon {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
  }
</style>
