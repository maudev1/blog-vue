<template>
  <div class="form">
    <div class="field">
      <div class="control">
        <label class="label">E-mail</label>

        <input class="is-default input" type="email" v-model="email" />
      </div>
    </div>

    <div class="field">
      <div class="control">
        <button @click="emailRegsiter" class="button" :class="isDefault">
          Enviar
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isDefault: "is-default",
      email: "",
    };
  },
  methods: {
    emailRegsiter() {
      if (this.email) {
        if (this.email.includes("@")) {
          this.$emit("SendMessage", this.email);
        } else {
          this.$emit("SendMessage", "Formato de e-mail inválido!");
        }
      } else {
        this.$emit("SendMessage", "Informe o e-mail!");
      }
    },
  },
};
</script>
