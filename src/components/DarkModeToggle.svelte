<script>
    import { onMount } from 'svelte';

    const STORAGE_KEY = 'theme';
    const DARK_PREFERENCE = '(prefers-color-scheme: dark)';
    
    const THEMES = {
      DARK: 'dark',
      LIGHT: 'light',
    };
  
    let currentTheme;
    const prefersDarkThemes = () => window.matchMedia(DARK_PREFERENCE).matches;
  
    const toggleTheme = () => {
      const stored = localStorage.getItem(STORAGE_KEY);
      if (stored) {
        // clear storage
        localStorage.removeItem(STORAGE_KEY);
      } else {
        // store opposite of preference
        localStorage.setItem(STORAGE_KEY, prefersDarkThemes() ? THEMES.LIGHT : THEMES.DARK);
      }
      applyTheme();
    };

    const applyTheme = () => {
        const preferredTheme = prefersDarkThemes() ? THEMES.DARK : THEMES.LIGHT;
        currentTheme = localStorage.getItem(STORAGE_KEY) ?? preferredTheme;
        if (currentTheme === THEMES.DARK) {
            document.body.classList.remove(THEMES.LIGHT);
            document.body.classList.add(THEMES.DARK);
        } else {
            document.body.classList.remove(THEMES.DARK);
            document.body.classList.add(THEMES.LIGHT);
        }
    };

    onMount(() => {
        applyTheme();
        window.matchMedia(DARK_PREFERENCE).addEventListener('change', applyTheme);
    });
</script>

<input id="darkToggle" class="darkToggle" type="checkbox" checked={currentTheme !== THEMES.DARK} on:click={toggleTheme} />


<style>
    .darkToggle{
        position: absolute;
        top: 5px;
        right: 5px;
    }
</style>    