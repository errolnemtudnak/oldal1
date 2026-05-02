<script lang="ts">
  import Icon from '@iconify/svelte';
  import { onMount } from 'svelte';
  import { ageHelper } from '$lib/date';

  type SpotifyTrack = {
    isPlaying: boolean;
    title: string;
    artist: string;
    albumImageUrl: string;
    url: string;
  };

  let track = $state<SpotifyTrack | null>(null);
  let setupCategory = $state<'gep' | 'periferiak'>('gep');
  let activeTab = $state('about');

  let socialLinks = [
    { name: 'YouTube', url: 'https://www.youtube.com/@Erikrobi1', icon: 'mdi:youtube' },
    { name: 'Discord', url: 'https://discord.com/users/397059113709862932/', icon: 'ic:baseline-discord' },
    { name: 'Twitch', url: 'https://www.twitch.tv/erikrobi', icon: 'mdi:twitch' },
    { name: 'Instagram', url: 'https://www.instagram.com/erikrobi/', icon: 'mdi:instagram' },
    { name: 'Twitter/X', url: 'https://x.com/Erikrobi1', icon: 'mdi:twitter' },
    { name: 'Steam', url: 'https://steamcommunity.com/id/erikrobi', icon: 'mdi:steam' }
  ];

  let techSpecs = [
    'Számítógépépítés',
    'Hardveres segítségnyújtás',
    'Villanyszerelés'
  ];

  let setupSpecs = [
    'NZXT H6 Flow',
    'Seasonic VERTEX 1000W 80+ Gold',
    'MSI MPG Carbon X870E',
    'Ryzen 7 9800X3D 8-Core 4.7GHz',
    'Arctic Freezer III 360 A-RGB',
    '2x Arctic P14 PWM PST ARGB',
    '4x Arctic P12 PWM PST ARGB',
    'Samsung 9100 PRO 1TB',
    'Samsung 990 EVO PLUS 1TB',
    'Kingston A2000 500GB',
    'G.SKILL Trident Z5 Neo RGB 2x16GB 6000MHz CL30',
    'MSI RTX 5070 TI Gaming Trio 16GB',
  ];

  let peripheralSpecs = [
    'HyperX Alloy Origins PBT UK',
    'HyperX PulseFire Haste 2 Wireless',
    'HyperX SoloCast',
    'Endorfy Studio Boom Arm',
    'iiyama G-MASTER GB3290QSU-B1 32',
    'iiyama G-MASTER G2741HSU-B1 27 (2x)'
  ];

  onMount(async () => {
    const res = await fetch('/spotify');
    track = await res.json();
  });
</script>

<svelte:head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com">
  <link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400;1,700&display=swap" rel="stylesheet">
</svelte:head>

<main class="min-h-screen bg-black text-white font-mono px-8 py-12">
  <!-- Header -->
  <header class="mb-12 text-center select-none">
    <h1 class="text-5xl md:text-7xl font-bold mb-4 tracking-wider pkosmos">
      ERIKROBI
    </h1>
    <div class="w-24 h-0.5 bg-white mx-auto mb-6"></div>
    <p class="text-xl text-gray-300">
      { ageHelper("2008/02/08") } éves • Magyarország • Villanyszerelő
    </p>
  </header>

  <!-- Tab navigation -->
  <nav class="mb-12">
    <div 
      class="flex flex-col sm:flex-row 
            justify-center items-center
            space-y-4 sm:space-y-0 sm:space-x-8
            select-none text-md"
    >
      <button 
        onclick={() => activeTab = 'about'}
        class="pb-2 border-b-2 transition-all duration-300 {activeTab === 'about' ? 'border-white text-white transform scale-105' : 'border-transparent text-gray-400 hover:text-white hover:scale-102'}"
      >
        [ ABOUT ]
      </button>
      <button 
        onclick={() => activeTab = 'setup'}
        class="pb-2 border-b-2 transition-all duration-300 {activeTab === 'setup' ? 'border-white text-white transform scale-105' : 'border-transparent text-gray-400 hover:text-white hover:scale-102'}"
      >
        [ SETUP ]
      </button>
      <button 
        onclick={() => activeTab = 'socials'}
        class="pb-2 border-b-2 transition-all duration-300 {activeTab === 'socials' ? 'border-white text-white transform scale-105' : 'border-transparent text-gray-400 hover:text-white hover:scale-102'}"
      >
        [ SOCIALS ]
      </button>
    </div>
  </nav>

  <!-- About Tab -->
  {#if activeTab === 'about'}
    <div class="max-w-2xl mx-auto text-center">
      <section class="mb-12 animate-fade-in select-none">
        <p class="text-gray-300 leading-relaxed mb-8 max-w-lg mx-auto">
          { ageHelper("2008/02/08") } éves, Tech rajongó. Digitális anyag és hardvergyűjtő.
        </p>
        
        <div class="mb-8">
          <h3 class="text-lg font-bold mb-4">SPECIALITÁSOK</h3>
          <ul class="space-y-2">
            {#each techSpecs as spec}
              <li class="text-gray-300">
                <span class="text-white">></span> {spec}
              </li>
            {/each}
          </ul>
        </div>
      </section>
    </div>
  {/if}

  <!-- Setup Tab -->
  {#if activeTab === 'setup'}
    <div class="max-w-3xl mx-auto">
      <section class="mb-12 animate-fade-in select-none">
        <!-- Category Toggle -->
        <div class="flex justify-center gap-6 mb-8 mt-1 text-center">
          <button 
            onclick={() => setupCategory = 'gep'}
            class="pb-2 border-b-2 transition-all duration-300 {setupCategory === 'gep' ? 'border-white text-white transform scale-105' : 'border-transparent text-gray-400 hover:text-white hover:scale-102'}"
          >
            <span class="text-sm">Gép</span>
          </button>
          <button 
            onclick={() => setupCategory = 'periferiak'}
            class="pb-2 border-b-2 transition-all duration-300 {setupCategory === 'periferiak' ? 'border-white text-white transform scale-105' : 'border-transparent text-gray-400 hover:text-white hover:scale-102'}"
          >
            <span class="text-sm">Perifériák</span>
          </button>
        </div>

        <!-- Specs list -->
        <div class="panel-color p-6 rounded border panel-border mb-8">
          <h3 class="text-lg font-bold mb-4">
            {setupCategory === 'gep' ? 'GÉP KONFIGURÁCIÓ' : 'PERIFÉRIÁK'}
          </h3>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-x-12 gap-y-4">
            {#if setupCategory === 'gep'}
              {#each setupSpecs as spec}
                <div class="text-gray-300">
                  <span class="text-white">></span> {spec}
                </div>
              {/each}
            {:else}
              {#each peripheralSpecs as spec}
                <div class="text-gray-300">
                  <span class="text-white">></span> {spec}
                </div>
              {/each}
            {/if}
          </div>
        </div>

        <div class="text-sm text-gray-500 text-center">
          > Utolsó frissítés: 2026-02-13
        </div>
      </section>
    </div>
  {/if}

  <!-- Socials Tab -->
  {#if activeTab === 'socials'}
    <div class="max-w-2xl mx-auto text-center">
      <section class="mb-12 animate-fade-in select-none">   
        <div class="flex flex-col lg:flex-row gap-8 items-stretch justify-center">
          <!-- Social Links -->
          <div class="flex-1 flex flex-col">
            <h3 class="text-lg font-bold mb-4">SOCIAL MEDIA</h3>
            <div class="grid grid-cols-2 gap-4 flex-1">
              {#each socialLinks as link}
                <a 
                  href={link.url} 
                  class="panel-color border panel-border p-4 rounded hover:bg-gray-800 hover:border-white transition-all duration-200 group"
                  target="_blank"
                  rel="noopener noreferrer"
                >
                  <div class="text-2xl mb-2 group-hover:scale-110 transition-transform">
                    <Icon icon={link.icon} class="w-6 h-6 mx-auto" />
                  </div>
                  <div class="text-sm text-gray-300 group-hover:text-white">
                    {link.name}
                  </div>
                </a>
              {/each}
            </div>
          </div>

          <!-- Spotify -->
          <div class="flex-1 flex flex-col">
            <h3 class="text-lg font-bold mb-4">SPOTIFY</h3>
            <div class="panel-color border panel-border rounded p-6 flex flex-col justify-center items-center flex-1">
              <!-- Spotify Profile Link -->
              <a 
                href="https://open.spotify.com/user/da9rr86191kzfwh4yxje028ho" 
                target="_blank" 
                rel="noopener noreferrer"
                class="mb-4 hover:scale-110 transition-transform"
              >
                <Icon icon="mdi:spotify" class="w-12 h-12 text-green-400" />
              </a>

              {#if track}
                {#if track.isPlaying}
                  <div class="text-sm text-gray-300 mb-2">Jelenleg lejátszott</div>
                {:else}
                  <div class="text-sm text-gray-300 mb-2">Legutóbb lejátszott</div>
                {/if}

                <!-- Song Link -->
                <a 
                  href={track.url} 
                  target="_blank" 
                  rel="noopener noreferrer"
                  class="panel-color-fg border panel-border rounded p-4 flex flex-col items-center w-[240px] hover:bg-gray-800 transition-colors"
                >
                  <img
                    src={track.albumImageUrl}
                    alt="album art"
                    class="w-20 h-20 mb-3 rounded-lg shadow-lg object-cover"
                    draggable="false"
                  />
                  <div class="text-xs text-gray-400 text-center truncate max-w-[200px]">{track.title}</div>
                  <div class="text-xs text-gray-500 text-center truncate max-w-[200px]">{track.artist}</div>
                </a>
              {:else}
                <p class="text-sm opacity-60">loading... (・-・)</p>
              {/if}
            </div>
          </div>
        </div>
      </section>
    </div>
  {/if}

  <!-- Footer -->
  <footer class="pt-8 border-t border-gray-700 max-w-2xl mx-auto text-center mt-12 select-none">
    <div class="flex flex-wrap items-center justify-center gap-x-2 text-gray-500 text-sm">
      <span>© 2026 Erikrobi és Társa Bt.</span>
      <span>|</span>
      <span>made with ❤️ by</span>
      <a 
        href="https://techy.hu" 
        target="_blank" 
        rel="noopener noreferrer" 
        class="hover:scale-110 transition-transform"
      >
        techy
      </a>
      in
      <Icon icon="ri:svelte-fill" width="18" height="18" />
    </div>
  </footer>
</main>
