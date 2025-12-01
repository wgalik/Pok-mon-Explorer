# Pokémon Explorer

A simple and interactive Pokémon Explorer built with Vue 3 (Composition API).
The app allows users to browse Pokémon by type, search by name, and load more results dynamically using the public PokeAPI.

## 📸 Demo

[Link](https://wgalik.github.io/Pok-mon-Explorer/)

## 🚀 Features

- Search Pokémon by name or type
- Filter buttons for all Pokémon types (Fire, Water, Electric, etc.)
- Dynamic Pokémon cards showing:
  - Name
  - Official artwork
  - Type(s)
  - Pokémon serial number
- Load more functionality (pagination-like behavior)
- Clean UI built with simple styling and Tailwind-like utility classes
- Modular Vue components:
  - ButtonComponent.vue
  - PokemonCard.vue
  - HelloWorld.vue

## 🧩 Technologies Used

- Vue 3 with <script setup>
- Composition API (ref, computed, onMounted)
- PokeAPI (https://pokeapi.co/)
- Fetch API for data loading
- Basic CSS / utility classes

## 📁 Project Structure (Key Components)

**App.vue**

- Handles global state:
  - Pokémon list
  - Search text
  - Limit of displayed cards
- Fetches Pokémon by type or search term
- Renders:
  - Search bar
  - Type buttons
  - Pokémon card list
  - "Load more" button

**ButtonComponent.vue**

- Reusable button component for type filters
- Receives:
  - text (button label)
- Emits click events used to trigger Pokémon fetches

**PokemonCard.vue**

- Fetches detailed Pokémon data from its individual URL
- Displays:
  - Name
  - Image
  - Serial number
  - Type(s)
- Background color changes dynamically based on Pokémon type

## API Usage

The app uses two PokeAPI endpoints:

Fetch Pokémon by type:
`https://pokeapi.co/api/v2/type/{type}`

Fetch single Pokémon:
`https://pokeapi.co/api/v2/pokemon/{id}`

## 📦 Installation & Setup

```
# Install dependencies
npm install

# Run development server
npm run dev

# Build for production
npm run build
```
