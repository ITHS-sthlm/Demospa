<script>
export default {
  data() {
    return {
      PokemonName: '',
      pokemon: null,
    };
  },
  methods: {
    async fetchData() {
      try {
        const lowercaseName = this.PokemonName.toLowerCase();
        const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${lowercaseName}`);
        const result = await response.json();
        this.pokemon = result;
        this.image = result.sprites.front_default;
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
    onClick() {
      this.fetchData();
    },
  },
};
</script>

<template>
  <div id="SearchBar">
    <div id="searchbox">
      <h2>Who's that Pokémon?</h2>
      <div class="SearchHere">
        <input id="title" v-model="PokemonName" placeholder="Enter Pokémon" />
        <input id="search" @click="onClick" type="button" value="Search" />
        <div id="answer" v-if="pokemon">
          <h3>It's {{pokemon.name}}!</h3>
          <ul>
            <li>Height: {{ pokemon.height }}0 cm </li>
            <li>Weight: {{ pokemon.weight }} Hecto</li>
            <li>Index number: {{ pokemon.id }} </li>
          </ul>
          <img :src="pokemon.sprites.front_default" alt="Pokemon Image" />
        </div>
      </div>
    </div>
  </div>
</template>
<template>
    <div>
      <v-container>
        <v-row>
          <v-col v-for="item in jsonData" :key="item.id" cols="12" sm="6" md="4">
            <v-card>
              <v-img :src="getImagePath(item.image)" alt="Bild"></v-img>
              <v-card-title>{{ item.name }}</v-card-title>
              <!-- Lägg till annan information om det behövs -->
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </div>
  </template>

  <script>
  import jsonData from '@/sökväg/till/din/lokala/json/fil.json'; // Uppdatera sökvägen

  export default {
    data() {
      return {
        jsonData: jsonData,
      };
    },
    methods: {
      getImagePath(imageFilename) {
        return require(`@/sökväg/till/din/images/mapp/${imageFilename}`); // Uppdatera sökvägen
      },
    },
  };
  </script>
<template>
    <div>
      <v-container>
        <v-row>
          <v-col v-for="item in jsonData" :key="item.id" cols="12" sm="6" md="4">
            <v-card>
              <v-img :src="getImagePath(item.image)" alt="Bild"></v-img>
              <v-card-title>{{ item.name }}</v-card-title>
              <!-- Lägg till annan information om det behövs -->
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </div>
  </template>
Här är ett exempel på hur du kan visa bilder från en lokal mapp i din Vue.js-komponent med Vuetify. Anta att du har en mapp "images" som innehåller dina bilder och en lokal JSON-fil som refererar till dessa bilder:

```html
<template>
  <div>
    <v-container>
      <v-row>
        <v-col v-for="item in jsonData" :key="item.id" cols="12" sm="6" md="4">
          <v-card>
            <v-img :src="getImagePath(item.image)" alt="Bild"></v-img>
            <v-card-title>{{ item.name }}</v-card-title>
            <!-- Lägg till annan information om det behövs -->
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import jsonData from '@/sökväg/till/din/lokala/json/fil.json'; // Uppdatera sökvägen

export default {
  data() {
    return {
      jsonData: jsonData,
    };
  },
  methods: {
    getImagePath(imageFilename) {
      return require(`@/sökväg/till/din/images/mapp/${imageFilename}`); // Uppdatera sökvägen
    },
  },
};
</script>
```

I detta exempel:

- `jsonData` är en array som innehåller din lokala JSON-data.
- Metoden `getImagePath` används för att dynamiskt generera sökvägen för varje bild baserat på filnamnet som finns i din JSON-fil.
- Komponenten `<v-img>` från Vuetify används för att visa bilderna.

Se till att uppdatera sökvägarna och filnamnen enligt din projektstruktur och namngivningskonventioner. Symbolen `@` är en förkortning för katalogen `src` i Vue.js-projekt. Justera sökvägarna baserat på din projektkonfiguration.
