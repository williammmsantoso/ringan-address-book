<template>
  <div class="popup-dialog-wrapper show" v-if="selectedContact && showDetail">
    <div class="backdrop" @click="updateShowDetail(false)">&nbsp;</div>
    <div class="modal">
        <div class="modal-content">
            <h2>Contact Detail</h2>
            <div v-if="editMode">
                <div class="input-wrapper">
                    <label>Name</label>
                    <input v-model="tempContact.name" />
                </div>
                
                <div class="input-wrapper">
                    <label>Email</label>
                    <input v-model="tempContact.email" />
                </div>

                <div class="input-wrapper">
                    <label>Phone</label>
                    <input v-model="tempContact.phone" />
                </div>                
                
                <div class="button-default" @click="saveChanges">Save</div>
                <div class="button-default type-red" @click="cancelEdit">Cancel</div>
            </div>
            <div v-else>
                <p>Name: {{ selectedContact.name }}</p>
                <p>Email: {{ selectedContact.email }}</p>
                <p>Phone: {{ selectedContact.phone }}</p>
                <div class="button-default" @click="handleClickEdit">Edit</div>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    selectedContact: Object,
    showDetail: Boolean
  },
  data() {
    return {
      editMode: false,
      tempContact: { ...this.selectedContact }, // Clone the selectedContact
    };
  },
  methods: {
    handleClickEdit() {
        this.editMode = true;
        this.tempContact = {
            name: this.selectedContact.name,
            email: this.selectedContact.email,
            phone: this.selectedContact.phone,
        }
    },
    saveChanges() {
      this.$emit("update-contact", this.selectedContact.id, this.tempContact);
      this.editMode = false;
      this.updateShowDetail(false);
    },
    cancelEdit() {
      this.editMode = false;
      this.tempContact = { ...this.selectedContact }; // Reset tempContact
    },
    updateShowDetail(value) {
        this.$emit("update-show-detail", value);
    }
  },
};
</script>


<style scoped>
/* Add your styling here */
</style>
