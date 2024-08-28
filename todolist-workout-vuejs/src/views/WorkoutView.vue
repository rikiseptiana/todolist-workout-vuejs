<!-- src/views/WorkoutView.vue -->
<template>
  <div class="min-h-screen bg-gray-100 p-4">
    <div class="max-w-lg mx-auto bg-white shadow-lg rounded-lg p-6">
      <h1 class="text-2xl font-bold mb-4 text-center">
        Jadwal Latihan 1 Bulan
      </h1>

      <!-- Filter dan Pencarian -->
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Cari latihan..."
        class="w-full p-2 mb-4 border rounded"
      />
      <label class="flex items-center space-x-2 mb-4">
        <input
          type="checkbox"
          v-model="showCompleted"
          class="form-checkbox h-5 w-5 text-blue-600"
        />
        <span>Tampilkan Hanya Latihan yang Selesai</span>
      </label>

      <!-- Jadwal Latihan Mingguan -->
      <div v-for="(week, index) in filteredWorkouts" :key="index" class="mb-6">
        <h2 class="text-xl font-semibold mb-2">Minggu {{ index + 1 }}</h2>
        <ul class="space-y-2">
          <li
            v-for="(day, i) in week.days"
            :key="i"
            class="flex items-center justify-between p-2 border rounded"
            :class="{ 'bg-green-100': day.completed }"
          >
            <span :class="{ 'line-through': day.completed }"
              >{{ day.day }}: {{ day.workout }}</span
            >
            <input
              type="checkbox"
              v-model="day.completed"
              @change="saveToLocalStorage"
              class="form-checkbox h-5 w-5 text-blue-600"
            />
          </li>
        </ul>
      </div>

      <!-- Tombol Kembali -->
      <router-link to="/">
        <button
          class="mt-4 bg-gray-500 text-white px-4 py-2 rounded hover:bg-gray-600"
        >
          Kembali
        </button>
      </router-link>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, watch } from "vue";

// State untuk Daftar Latihan
const workouts = ref([
  {
    week: 1,
    days: [
      {
        day: "Senin",
        workout: "HIIT Kardio: Jumping Jacks, Mountain Climbers, Burpees",
        completed: false,
      },
      {
        day: "Selasa",
        workout:
          "Latihan Inti: Plank, Russian Twists, Leg Raises, Bicycle Crunches",
        completed: false,
      },
      {
        day: "Rabu",
        workout:
          "Kombinasi Kardio & Inti: High Knees, Flutter Kicks, Skaters, Heel Touches",
        completed: false,
      },
      {
        day: "Kamis",
        workout: "HIIT Kardio: Jumping Jacks, Mountain Climbers, Burpees",
        completed: false,
      },
      {
        day: "Jumat",
        workout:
          "Latihan Inti: Plank, Russian Twists, Leg Raises, Bicycle Crunches",
        completed: false,
      },
      {
        day: "Sabtu",
        workout: "Yoga/Streching: Yoga Flow untuk fleksibilitas dan pernapasan",
        completed: false,
      },
      {
        day: "Minggu",
        workout: "Istirahat Aktif: Jalan kaki santai atau stretching ringan",
        completed: false,
      },
    ],
  },
  {
    week: 2,
    days: [
      {
        day: "Senin",
        workout: "Kardio Lanjutan: Burpees, High Knees, Jump Rope",
        completed: false,
      },
      {
        day: "Selasa",
        workout: "Latihan Inti Intensif: Side Plank, V-Ups, Mountain Climbers",
        completed: false,
      },
      {
        day: "Rabu",
        workout:
          "HIIT Kardio & Inti: Jumping Jacks, Leg Raises, Bicycle Crunches",
        completed: false,
      },
      {
        day: "Kamis",
        workout: "Kardio Lanjutan: Burpees, High Knees, Jump Rope",
        completed: false,
      },
      {
        day: "Jumat",
        workout: "Latihan Inti Intensif: Side Plank, V-Ups, Mountain Climbers",
        completed: false,
      },
      {
        day: "Sabtu",
        workout: "Yoga/Streching: Yoga Flow untuk fleksibilitas dan pernapasan",
        completed: false,
      },
      {
        day: "Minggu",
        workout: "Istirahat Aktif: Jalan kaki santai atau stretching ringan",
        completed: false,
      },
    ],
  },
  {
    week: 3,
    days: [
      {
        day: "Senin",
        workout: "HIIT Ekstra Intensif: Sprint, Burpees, Jump Lunges",
        completed: false,
      },
      {
        day: "Selasa",
        workout:
          "Latihan Inti Lanjutan: Russian Twists, Heel Touches, Leg Raises",
        completed: false,
      },
      {
        day: "Rabu",
        workout: "HIIT Kardio & Inti: High Knees, Plank Jacks, Skaters",
        completed: false,
      },
      {
        day: "Kamis",
        workout: "HIIT Ekstra Intensif: Sprint, Burpees, Jump Lunges",
        completed: false,
      },
      {
        day: "Jumat",
        workout:
          "Latihan Inti Lanjutan: Russian Twists, Heel Touches, Leg Raises",
        completed: false,
      },
      {
        day: "Sabtu",
        workout: "Yoga/Streching: Yoga Flow untuk fleksibilitas dan pernapasan",
        completed: false,
      },
      {
        day: "Minggu",
        workout: "Istirahat Aktif: Jalan kaki santai atau stretching ringan",
        completed: false,
      },
    ],
  },
  {
    week: 4,
    days: [
      {
        day: "Senin",
        workout: "Kardio & Inti Intensif: Burpees, V-Ups, Jump Squats",
        completed: false,
      },
      {
        day: "Selasa",
        workout: "Latihan Inti Terfokus: Plank, Leg Raises, Side Plank",
        completed: false,
      },
      {
        day: "Rabu",
        workout: "HIIT Kardio: Jump Rope, Skaters, Mountain Climbers",
        completed: false,
      },
      {
        day: "Kamis",
        workout: "Kardio & Inti Intensif: Burpees, V-Ups, Jump Squats",
        completed: false,
      },
      {
        day: "Jumat",
        workout: "Latihan Inti Terfokus: Plank, Leg Raises, Side Plank",
        completed: false,
      },
      {
        day: "Sabtu",
        workout: "Yoga/Streching: Yoga Flow untuk fleksibilitas dan pernapasan",
        completed: false,
      },
      {
        day: "Minggu",
        workout: "Istirahat Aktif: Jalan kaki santai atau stretching ringan",
        completed: false,
      },
    ],
  },
]);

// Fungsi untuk Menyimpan ke Local Storage
const saveToLocalStorage = () => {
  localStorage.setItem("workouts", JSON.stringify(workouts.value));
};

// Mengambil Data dari Local Storage Saat Komponen Dimuat
onMounted(() => {
  const savedWorkouts = localStorage.getItem("workouts");
  if (savedWorkouts) {
    workouts.value = JSON.parse(savedWorkouts);
  }
});

// Mengawasi Perubahan dan Menyimpan ke Local Storage
watch(workouts, saveToLocalStorage, { deep: true });

// State untuk Pencarian dan Filter
const searchQuery = ref("");
const showCompleted = ref(false);

// Menggunakan computed untuk Filter dan Pencarian
const filteredWorkouts = computed(() => {
  return workouts.value.map((week) => ({
    ...week,
    days: week.days.filter((day) => {
      const matchesSearch = day.workout
        .toLowerCase()
        .includes(searchQuery.value.toLowerCase());
      const matchesCompletion = showCompleted.value ? day.completed : true;
      return matchesSearch && matchesCompletion;
    }),
  }));
});
</script>

<style scoped>
.line-through {
  text-decoration: line-through;
}
</style>
