<script setup lang="ts">
import router from "../../router";
import axios from "axios";
import { onMounted, ref } from "vue";
import type { ServerReview } from "@/types/review";
import RatingStars from "@/components/RatingStars/RatingStars.vue";
import doctor from "@/assets/images/doctors/2.jpg";

const id = router.currentRoute.value.params.id;
const review = ref<ServerReview>({
  id: 0,
  name: "",
  body: "",
  postId: 0,
  email: ""
});

const fetchReview = async () => {
  try {
    const { data } = await axios.get(`https://jsonplaceholder.typicode.com/comments/${id}`);
    review.value = data;
  } catch (error) {
    alert("Something went wrong. Please try again later.");
  }
};

onMounted(() => {
  fetchReview();
});

</script>

<template>
  <v-container class="container review-container">
    <v-row>
      <v-col>
        <h1 class="doctor-name">Dr. John Doe</h1>
      </v-col>
    </v-row>
    <v-row>
      <v-col class="d-flex justify-lg-space-between mb-3">
        <rating-stars :rating="4" />
        <p class="recommended-text">recommended by 84% of patients</p>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6" md="4">
        <v-img :src="doctor" alt="Doctor Image" class="doctor-img" />
      </v-col>
      <v-col cols="6" md="8">
        <div class="review-details">
          <p><strong class="label">Doctor:</strong> Dr. Peter Parker</p>
          <p><strong class="label">Speciality:</strong> Psychotherapist</p>
          <p><strong class="label">Clinic:</strong> Hermes Medical Center, 33, 5th Avenue, New York, NY 10003
          </p>
        </div>
      </v-col>
    </v-row>
    <v-divider class="section-divider" />
    <v-row class="patient-info">
      <v-col>
        <p class="label">Patient</p>
        <p>{{ review.email }}</p>
      </v-col>
      <v-col>
        <p class="label">Appointment Date</p>
        <p>12/12/2020</p>
      </v-col>
    </v-row>
    <v-divider class="section-divider" />
    <v-row class="review-section">
      <v-col>
        <p class="reviewer-name">{{ review.name }}</p>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <p>{{ review.body }}</p>
      </v-col>
    </v-row>
    <v-divider class="section-divider" />
    <v-row>
      <v-col>
        <p class="label">Patient Feedback</p>
      </v-col>
      <v-col>
        <rating-stars :rating="5" />
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>

.review-container{
  max-width: 900px;
}

.doctor-name {
  font-size: 24px;
  color: var(--indigo);
}

.recommended-text {
  color: var(--success);
  margin-left: 10px;
}

.doctor-img {
  width: 100%;
  max-width: 200px;
  border-radius: 8px;
}

.section-divider {
  margin: 20px 0;
}

.reviewer-name {
  font-weight: bold;
  font-size: 18px;
  color: var(--secondary);
}

.label {
  font-size: 18px;
  color: var(--secondary);
}
</style>