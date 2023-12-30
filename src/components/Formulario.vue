<script setup>
import { computed, reactive } from "vue";
import Alerta from "../components/Alerta.vue";

const alerta = reactive({
  type: "",
  message: "",
});

const emit = defineEmits([
  "update:nombre",
  "update:propietario",
  "update:email",
  "update:alta",
  "update:sintomas",
  "guardar-paciente",
]);

const props = defineProps({
  id: {
    type: [String, null],
    required: true,
  },
  nombre: {
    type: String,
    required: true,
  },
  propietario: {
    type: String,
    required: true,
  },
  email: {
    type: String,
    required: true,
  },
  alta: {
    type: String,
    required: true,
  },
  sintomas: {
    type: String,
    required: true,
  },
});

const validar = () => {
  if (Object.values(props).includes("")) {
    alerta.message = "Todos los campos son obligatorios";
    alerta.type = "error";
    return;
  }

  emit("guardar-paciente");
  alerta.message = "Paciente almacenado correctamente";
  alerta.type = "exito";

  //Reiniciar el mensaje
  setTimeout(() => {
    // alerta.message = "";
    Object.assign(alerta, {
      type: "",
      message: "",
    });
  }, 3000);
};

const editando = computed(() => {
  return props.id;
});
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center">Seguimirnto pacientes</h2>

    <p class="text-lg mt-5 text-center mb-10">
      Añade pacientes y
      <span class="text-green-500 font-bold">Administralos</span>
    </p>

    <Alerta v-if="alerta.message" :alerta="alerta" />
    <form
      @submit.prevent="validar"
      class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
    >
      <div class="mb-5">
        <label for="mascota" class="block text-gray-700 uppercase font-bold">
          Nombre mascota
        </label>

        <input
          id="mascota"
          type="text"
          placeholder="Nombre de la mascota"
          class="border-2 w-full p-2 mt-2 rounded-lg outline-gray-500 placeholder-gray-500"
          :value="nombre"
          @input="$emit('update:nombre', $event.target.value)"
        />
      </div>
      <div class="mb-5">
        <label
          for="propietario"
          class="block text-gray-700 uppercase font-bold"
        >
          Nombre propietario
        </label>

        <input
          type="text"
          id="propietario"
          placeholder="Nombre del propietario"
          class="border-2 w-full p-2 mt-2 rounded-lg outline-gray-500 placeholder-gray-500"
          :value="propietario"
          @input="$emit('update:propietario', $event.target.value)"
        />
      </div>
      <div class="mb-5">
        <label for="email" class="block text-gray-700 uppercase font-bold">
          Email
        </label>

        <input
          type="email"
          id="email"
          placeholder="Nombre del email"
          class="border-2 w-full p-2 mt-2 rounded-lg outline-gray-500 placeholder-gray-500"
          :value="email"
          @input="$emit('update:email', $event.target.value)"
        />
      </div>
      <div class="mb-5">
        <label for="alta" class="block text-gray-700 uppercase font-bold">
          Fecha alta
        </label>

        <input
          type="date"
          id="alta"
          class="border-2 w-full p-2 mt-2 rounded-lg outline-gray-500 placeholder-gray-500"
          :value="alta"
          @input="$emit('update:alta', $event.target.value)"
        />
      </div>
      <div class="mb-5">
        <label for="sintomas" class="block text-gray-700 uppercase font-bold">
          Sintomas
        </label>

        <textarea
          id="sintomas"
          placeholder="Ingrese sintomas"
          class="border-2 w-full p-2 mt-2 rounded-lg outline-gray-500 placeholder-gray-500 h-28"
          :value="sintomas"
          @input="$emit('update:sintomas', $event.target.value)"
        />
      </div>

      <input
        type="submit"
        class="bg-green-500 w-full p-3 text-white uppercase font-bold hover:bg-green-600 cursor-pointer transition-colors rounded-lg"
        :value="[editando ? 'Guardar cambios' : 'Registrar paciente']"
      />
    </form>
  </div>
</template>
