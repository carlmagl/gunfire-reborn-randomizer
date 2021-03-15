<script>
  export let weaponClasses;
  import Weapon from "../components/Weapon.svelte";
  $: weapons = () => {
    let weapons = [];
    let tempWeapons = [...weaponClasses];
    weapons[0] = tempWeapons.splice(getRandomInt(tempWeapons.length), 1);
    weapons[1] = tempWeapons.splice(getRandomInt(tempWeapons.length), 1);
    return weapons;
  };
  function getRandomInt(max) {
    return Math.floor(Math.random() * Math.floor(max));
  }
</script>

<main>
  <div>
    <h3>Weapons</h3>
    {#each weapons() as weapon}
      <Weapon weapon={weapon[0]} />
    {/each}
  </div>
</main>

<style>
</style>
