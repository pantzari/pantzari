<script setup>
import { ref } from "vue";

const moods = [
  { id: "great", emoji: "😄", label: "Great" },
  { id: "good", emoji: "🙂", label: "Good" },
  { id: "okay", emoji: "😐", label: "Okay" },
  { id: "low", emoji: "😔", label: "Low" },
  { id: "rough", emoji: "😣", label: "Rough" },
];

const selectedMood = ref("");
const today = new Date().toLocaleDateString("en-CA");
const entryDate = ref(today);
const note = ref("");
const entries = ref([]);
function saveEntry() {
  if (!selectedMood.value || !entryDate.value) {
    return;
  }

  const entry = {
    id: Date.now(),
    date: entryDate.value,
    moodId: selectedMood.value,
    note: note.value.trim(),
  };

  entries.value.unshift(entry);

  selectedMood.value = "";
  note.value = "";
  entryDate.value = today;
}
</script>

<template>
  <main class="app">
    <header class="header">
      <p class="eyebrow">YOUR PERSONAL SPACE</p>
      <h1>moodspace ☁️</h1>
      <p class="subtitle">Your feelings, one day at a time.</p>
    </header>

    <section class="card">
      <h2>How are you feeling?</h2>
      <p class="hint">There's no right or wrong answer.</p>

      <div class="moods">
        <button
          v-for="mood in moods"
          :key="mood.id"
          type="button"
          class="mood"
          :class="{ selected: selectedMood === mood.id }"
          :aria-pressed="selectedMood === mood.id"
          @click="selectedMood = mood.id"
        >
          <span class="emoji">{{ mood.emoji }}</span>
          <span>{{ mood.label }}</span>
        </button>
      </div>

      <div class="form-group">
        <label for="entry-date">Date</label>
        <input id="entry-date" v-model="entryDate" type="date" />
      </div>

      <div class="form-group">
        <label for="note">What's on your mind?</label>
        <textarea
          id="note"
          v-model="note"
          placeholder="Write as much or as little as you want..."
          rows="4"
        ></textarea>
      </div>

      <button
        class="save-button"
        :disabled="!selectedMood || !entryDate"
        @click="saveEntry"
      >
        Save mood
      </button>
    </section>

    <section class="card">
      <h2>Recent entries</h2>

      <p v-if="entries.length === 0" class="empty">
        No entries yet. Your first check-in starts here!
      </p>

      <div v-else class="entries">
        <article v-for="entry in entries" :key="entry.id" class="entry">
          <p class="entry-date">{{ entry.date }}</p>

          <p class="entry-mood">
            {{ moods.find((mood) => mood.id === entry.moodId)?.emoji }}
            {{ moods.find((mood) => mood.id === entry.moodId)?.label }}
          </p>

          <p v-if="entry.note" class="entry-note">
            {{ entry.note }}
          </p>
        </article>
      </div>
    </section>
  </main>
</template>
