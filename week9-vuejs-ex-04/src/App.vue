<template>
  <div class="app">

    <!-- Header -->
    <header>
      <h1>💪 FlexZone Fitness</h1>
      <p>Total Sessions: {{ totalSessions }}</p>
    </header>

    <!-- Add Class Form -->
    <div class="form-card">
      <h2>Add New Class</h2>

      <p v-if="errorMessage" class="error">{{ errorMessage }}</p>

      <label>Class Name</label>
      <input v-model="newClass.name" placeholder="e.g. Yoga" />

      <label>Coach</label>
      <input v-model="newClass.coach" placeholder="e.g. Sarah" />

      <label>Date</label>
      <input v-model="newClass.date" type="date" />

      <label>Time</label>
      <input v-model="newClass.time" type="time" />

      <label>Capacity</label>
      <input v-model="newClass.capacity" type="number" placeholder="e.g. 20" />

      <button @click="addClass">Add Session</button>
    </div>

    <!-- Sessions List -->
    <div class="sessions">
      <h2>Scheduled Sessions</h2>

      <!-- Show this if no sessions -->
      <p v-if="sessions.length === 0" class="empty">
        No sessions scheduled yet. Add one above!
      </p>

      <!-- Loop through sessions -->
      <div v-for="(session, index) in sessions" :key="index" class="session-card">
        <div class="session-info">
          <h3>{{ session.name }}</h3>
          <p>👤 Coach: {{ session.coach }}</p>
          <p>📅 Date: {{ session.date }}</p>
          <p>🕐 Time: {{ session.time }}</p>
          <p>👥 Capacity: {{ session.capacity }}</p>
        </div>
        <button class="delete-btn" @click="deleteSession(index)">Delete</button>
      </div>
    </div>

  </div>
</template>


<script>
export default {
  name: "App",

  data() {
    return {
      errorMessage: "",

      // Form fields
      newClass: {
        name: "",
        coach: "",
        date: "",
        time: "",
        capacity: ""
      },

      // List of sessions
      sessions: [
        {
          name: "Morning Yoga",
          coach: "Sarah",
          date: "2026-06-15",
          time: "07:00",
          capacity: 15
        },
        {
          name: "Spinning",
          coach: "Mike",
          date: "2026-06-15",
          time: "09:00",
          capacity: 20
        }
      ]
    };
  },

  computed: {
    // Automatically counts total sessions
    totalSessions() {
      return this.sessions.length;
    }
  },

  methods: {
    addClass() {
      // Validation - check all fields are filled
      if (
        this.newClass.name === "" ||
        this.newClass.coach === "" ||
        this.newClass.date === "" ||
        this.newClass.time === "" ||
        this.newClass.capacity === ""
      ) {
        this.errorMessage = "Please fill in all fields before adding a session.";
        return;
      }

      // Clear error and add session
      this.errorMessage = "";
      this.sessions.push({
        name: this.newClass.name,
        coach: this.newClass.coach,
        date: this.newClass.date,
        time: this.newClass.time,
        capacity: this.newClass.capacity
      });

      // Reset form
      this.newClass = { name: "", coach: "", date: "", time: "", capacity: "" };
    },

    deleteSession(index) {
      this.sessions.splice(index, 1);
    }
  }
};
</script>


<style>
* { box-sizing: border-box; margin: 0; padding: 0; }

body { font-family: Arial, sans-serif; background: #f0f2f5; }

.app { max-width: 800px; margin: 0 auto; padding: 20px; }

header {
  background: #e74c3c;
  color: white;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.form-card {
  background: white;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.form-card h2 { margin-bottom: 15px; }

label {
  display: block;
  margin-top: 10px;
  font-weight: bold;
  font-size: 14px;
}

input {
  width: 100%;
  padding: 8px;
  margin-top: 4px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 14px;
}

button {
  margin-top: 15px;
  padding: 10px 20px;
  background: #e74c3c;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 15px;
  width: 100%;
}

.error {
  color: red;
  margin-bottom: 10px;
  font-size: 14px;
}

.sessions h2 { margin-bottom: 15px; }

.empty {
  text-align: center;
  color: #999;
  padding: 30px;
  background: white;
  border-radius: 8px;
}

.session-card {
  background: white;
  padding: 15px;
  border-radius: 8px;
  margin-bottom: 10px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.08);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.session-info h3 { margin-bottom: 5px; color: #e74c3c; }

.session-info p { font-size: 13px; color: #555; margin: 2px 0; }

.delete-btn {
  width: auto;
  background: #c0392b;
  padding: 8px 15px;
  margin: 0;
}
</style>