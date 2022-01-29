<script>
  import Hero from "./components/Hero.svelte";
  import Weapons from "./components/Weapons.svelte";
  import DarkModeToggle from "./components/DarkModeToggle.svelte";
  let heroes = [
    { name: "Crown Prince", imgUrl: "/heroes/Crown_Prince_Icon.png" },
    { name: "Ao Bai", imgUrl: "/heroes/Ao_Bai_Icon.png" },
    { name: "Qing Yan", imgUrl: "/heroes/Qing_Yan_Icon.png" },
    { name: "Lei Luo", imgUrl: "/heroes/Lei_Luo_Icon.png" },
    { name: "Tao", imgUrl: "/heroes/Tao_Icon.png" },
    { name: "Qian Sui", imgUrl: "/heroes/Qian_Sui_Icon.png" },
  ];
  let weaponClasses = [
    { name: "Rifles", imgUrl: "/weapons/Rifles.png" },
    { name: "Submachine guns", imgUrl: "/weapons/Submachine_Gun.png" },
    { name: "Pistols", imgUrl: "/weapons/Pistols.png" },
    { name: "Shotguns", imgUrl: "/weapons/Shotguns.png" },
    { name: "Snipers", imgUrl: "/weapons/Snipers.png" },
    { name: "Launchers", imgUrl: "/weapons/Launchers.png" },
    { name: "Injectors", imgUrl: "/weapons/Injectors.png" },
    { name: "Meele Weapons", imgUrl: "/weapons/Melee_Weapon.png" },
  ];
  let name = "";

  let users = [{ name: "Carl", id: 0 }, { name: "Petter", id: 1 }, { name: "Oliver", id: 2}];

  let removed = true;

  function getRandomInt(max) {
    return Math.floor(Math.random() * Math.floor(max));
  }

  function updateInfo() {
    heroes = [...heroes];
    weaponClasses = [...weaponClasses];
  }
  function removeMeleeWeapon() {
    if (removed)
      weaponClasses.push({
        name: "Meele Weapons",
        imgUrl: "/weapons/Melee_Weapon.png",
      });
    else {
      weaponClasses.splice(-1, 1);
    }
    updateInfo();
    removed = !removed;
  }

  const addUser = () => {
    if(name.length === 0) return 0; 
    users = [
      ...users,
      {
        id: users.length,
        name,
      }
    ];
    name = "";
  };
</script>

<main>
  <DarkModeToggle />
  <h1>Gunfire Reborn randomizer</h1>
  <p>Welcome to the gunfire reborn randomizer</p>
  <form on:submit|preventDefault={addUser}>
    <label for="name">Add a user</label>
    <input id="name" type="text" bind:value={name} />
  </form>
  <button on:click={() => updateInfo()}>Randomize</button>
  <div class="radio">
    <input
      type="checkbox"
      id="melee"
      class="collapsed"
      bind:checked={removed}
      on:click={() => removeMeleeWeapon()}
    />
    <label for="meele">Remove melee weapon</label>
  </div>
  {#if removed}
    <h3>Melee Weapons removed</h3>
  {/if}
  <section class="builds">
    {#each users as user}
      <div class="user">
        <button class="removeButton" on:click={() => {
          users = users.filter(x => x.id !== user.id);
        }}>X</button>
        <h2>{user.name}</h2>
        <Hero hero={heroes[getRandomInt(heroes.length)]} />
        <Weapons bind:weaponClasses />
      </div>
    {/each}
  </section>
</main>

<style>
  main {
    text-align: center;
    max-width: 240px;
    margin: 0 auto;
  }

  input {
    margin: 0;
    margin-right: 20px;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 3em;
    font-weight: 200;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
  .builds {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    align-items: stretch;
  }


  form {
    display: flex;
    justify-content: center;
    align-items: center;
    color: #777;
    margin-bottom: 10px;
  }

  label{
    margin-right: 5px;
  }

  .removeButton {
    position: absolute;
    top: 0;
    right: 0;
  }

  .user {
    position: relative;
    margin: 40px;
    padding: 0 60px;
    border-radius: 8px;
    border: solid;
    border-color: #809ead;
  }
  @media (prefers-color-scheme: dark) {
  body:not(.light) {

  }
}
  .radio {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
  }
</style>
