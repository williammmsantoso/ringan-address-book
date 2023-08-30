<template>
  <div class="popup-dialog-wrapper show" v-if="showAdd">
    <div class="backdrop" @click="updateShowAdd(false)">&nbsp;</div>
    <div class="modal">
        <div class="modal-content">
            <h2>{{ editingContact ? "Edit" : "Add" }} Contact</h2>
            <form @submit.prevent="saveContact">
                <div class="input-wrapper">
                    <label>Name: </label>
                    <input v-model="newContact.name" required />
                </div>
                <div class="input-wrapper">
                    <label>Email: </label>
                    <input v-model="newContact.email" type="email" required />
                </div>
                <div class="input-wrapper">
                    <label>Phone: </label>
                    <input v-model="newContact.phone" type="tel" required />
                </div>

                <button type="submit">
                    <div class="button-default">
                        {{ editingContact ? "Update" : "Save" }}
                    </div>
                </button>
            </form>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["contact", "showAdd"],
  data() {
    return {
      newContact: {
        name: "",
        email: "",
        phone: "",
      },
      editingContact: this.contact,
    };
  },
  methods: {
    saveContact() {
      if (this.editingContact) {
        this.$emit("update-contact", this.editingContact.id, this.newContact);
      } else {
        this.$emit("add-contact", this.newContact);
      }
      this.newContact = { name: "", email: "", phone: "" };
      this.editingContact = null; // Reset editingContact after saving
      this.updateShowAdd(false);
    },
    updateShowAdd(value) {
        this.$emit("update-show-add", value);
    }
  },
};
</script>


<style scoped>
button {
    background: none;
	color: inherit;
	border: none;
	padding: 0;
	font: inherit;
	cursor: pointer;
	outline: inherit;
    width: 100%;
}

.button-default {
    margin-top: 48px;
    margin-bottom: 0;
}
</style>
