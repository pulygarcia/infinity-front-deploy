<script setup>
    import AdminAppointment from '../../components/AdminAppointment.vue';
    import { useUserStore } from '../../stores/userStore';
    import Loader from '../../components/Loader.vue';

    const userStore = useUserStore();
</script>

<template>
  <p class="text-white mt-5">Aquí podés administrar tus próximos turnos</p>

  <Loader v-if="userStore.loading"/>

  <div v-else>
    <p v-if="!userStore.noAppointments" class="text-red-500 mt-10 text-center text-lg">No tienes turnos próximos</p>
  </div>
  
  <div v-else class="grid grid-cols-1 gap-5 mt-10">
    <AdminAppointment
      v-for="appointment in userStore.userAppointments"
      :key="appointment._id"
      :appointment="appointment"
      :user="appointment.user"
    />
  </div>
</template>