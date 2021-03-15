<script>
  import Hero from "./components/Hero.svelte";
  import Weapons from "./components/Weapons.svelte";
  const heroes = [
    { name: "Crown Prince", imgUrl: "/heroes/Crown_Prince_Icon.png" },
    { name: "Ao Bai", imgUrl: "/heroes/Ao_Bai_Icon.png" },
    { name: "Qing Yan", imgUrl: "/heroes/Qing_Yan_Icon.png" },
    { name: "Lei Luo", imgUrl: "/heroes/Lei_Luo_Icon.png" },
  ];
  const weaponClasses = [
    { name: "Rifles", imgUrl: "/weapons/Rifles.png" },
    { name: "Submachine guns", imgUrl: "/weapons/Submachine_Gun.png" },
    { name: "Pistols", imgUrl: "/weapons/Pistols.png" },
    { name: "Shotguns", imgUrl: "/weapons/Shotguns.png" },
    { name: "Snipers", imgUrl: "/weapons/Snipers.png" },
    { name: "Launchers", imgUrl: "/weapons/Launchers.png" },
    { name: "Injectors", imgUrl: "/weapons/Injectors.png" },
    { name: "Meele Weapons", imgUrl: "/weapons/Melee_Weapon.png" },
  ];

  let users = [{ name: "Carl" }, { name: "Petter" }, { name: "Oliver" }];

  function getRandomInt(max) {
    return Math.floor(Math.random() * Math.floor(max));
  }

  function addUser(name) {
    users = [...users, name];
  }
</script>

<main>
  <h1>Gunfire Reborn randomizer</h1>
  <p>Welcome to the gunfire reborn randomizer</p>
  <button />
  <section class="builds">
    {#each users as user}
      <div class="user">
        <h2>{user.name}</h2>
        <Hero hero={heroes[getRandomInt(heroes.length)]} />
        <Weapons {weaponClasses} />
      </div>
    {/each}
  </section>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
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

  .user {
    margin: 40px;
    padding: 0 60px;
    border-radius: 8px;
    border: solid;
    border-color: #809ead;
  }
</style>
