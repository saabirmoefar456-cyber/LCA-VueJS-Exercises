<template>
  <div class="app">

    <!-- Header -->
    <header>
      <h1>🏠 Homes & Beyond</h1>
      <p>{{ filteredProperties.length }} properties available</p>
    </header>

    <!-- Search and Sort -->
    <div class="controls">
      <input 
        v-model="searchQuery" 
        placeholder="Search by title or location..." 
      />
      <select v-model="sortOrder">
        <option value="">Sort by Price</option>
        <option value="low">Price: Low to High</option>
        <option value="high">Price: High to Low</option>
      </select>
    </div>

    <!-- Property Cards -->
    <div class="grid">
      <div 
        v-for="property in filteredProperties" 
        :key="property.id" 
        class="card"
        :class="{ unavailable: !property.available }"
      >
        <!-- Not Available Badge -->
        <div v-if="!property.available" class="ribbon">Not Available</div>

        <!-- Bookmark Button -->
        <button 
          class="bookmark" 
          @click="toggleBookmark(property)"
        >
          {{ property.bookmarked ? '❤️' : '🤍' }}
        </button>

        <img :src="property.image" :alt="property.title" />

        <div class="card-body">
          <h2>{{ property.title }}</h2>
          <p class="location">📍 {{ property.location }}</p>
          <p class="type">🏷️ {{ property.type }}</p>
          <p class="price">R{{ property.price }} / night</p>
        </div>
      </div>
    </div>

  </div>
</template>


<script>
export default {
  name: "App",

  // data() holds all our variables
  data() {
    return {
      searchQuery: "",
      sortOrder: "",

      properties: [
        {
          id: 1,
          title: "Sea Point Studio",
          location: "Sea Point, Cape Town",
          type: "Apartment",
          price: 850,
          available: true,
          bookmarked: false,
          image: "https://placehold.co/300x180?text=Sea+Point"
        },
        {
          id: 2,
          title: "Camps Bay Villa",
          location: "Camps Bay, Cape Town",
          type: "Villa",
          price: 3200,
          available: true,
          bookmarked: false,
          image: "https://placehold.co/300x180?text=Camps+Bay"
        },
        {
          id: 3,
          title: "Observatory Loft",
          location: "Observatory, Cape Town",
          type: "Loft",
          price: 620,
          available: false,
          bookmarked: false,
          image: "https://placehold.co/300x180?text=Observatory"
        },
        {
          id: 4,
          title: "Constantia Cottage",
          location: "Constantia, Cape Town",
          type: "Cottage",
          price: 1100,
          available: true,
          bookmarked: false,
          image: "https://placehold.co/300x180?text=Constantia"
        },
        {
          id: 5,
          title: "Green Point Flat",
          location: "Green Point, Cape Town",
          type: "Apartment",
          price: 950,
          available: false,
          bookmarked: false,
          image: "https://placehold.co/300x180?text=Green+Point"
        },
        {
          id: 6,
          title: "Woodstock Warehouse",
          location: "Woodstock, Cape Town",
          type: "Studio",
          price: 700,
          available: true,
          bookmarked: false,
          image: "https://placehold.co/300x180?text=Woodstock"
        }
      ]
    };
  },

  // computed properties automatically update when data changes
  computed: {
    filteredProperties() {
      let result = this.properties;

      // Filter by search query
      if (this.searchQuery !== "") {
        result = result.filter(property =>
          property.title.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          property.location.toLowerCase().includes(this.searchQuery.toLowerCase())
        );
      }

      // Sort by price
      if (this.sortOrder === "low") {
        result = result.slice().sort((a, b) => a.price - b.price);
      } else if (this.sortOrder === "high") {
        result = result.slice().sort((a, b) => b.price - a.price);
      }

      return result;
    }
  },

  // methods are functions
  methods: {
    toggleBookmark(property) {
      property.bookmarked = !property.bookmarked;
    }
  }
};
</script>


<style>
* { box-sizing: border-box; margin: 0; padding: 0; }

body { font-family: Arial, sans-serif; background: #f5f5f5; }

.app { max-width: 1100px; margin: 0 auto; padding: 20px; }

header {
  background: #2c3e50;
  color: white;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.controls {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.controls input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 15px;
}

.controls select {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 15px;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
}

.card {
  background: white;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  position: relative;
}

.card.unavailable {
  opacity: 0.6;
}

.ribbon {
  position: absolute;
  top: 10px;
  left: 10px;
  background: red;
  color: white;
  padding: 4px 10px;
  border-radius: 4px;
  font-size: 12px;
  font-weight: bold;
}

.bookmark {
  position: absolute;
  top: 10px;
  right: 10px;
  background: white;
  border: none;
  border-radius: 50%;
  width: 35px;
  height: 35px;
  font-size: 18px;
  cursor: pointer;
  box-shadow: 0 1px 4px rgba(0,0,0,0.2);
}

.card img {
  width: 100%;
  height: 180px;
  object-fit: cover;
}

.card-body { padding: 15px; }

.card-body h2 { margin-bottom: 8px; font-size: 18px; }

.location, .type { color: #666; font-size: 14px; margin-bottom: 4px; }

.price { 
  margin-top: 10px;
  font-size: 18px; 
  font-weight: bold; 
  color: #2c3e50; 
}
</style>