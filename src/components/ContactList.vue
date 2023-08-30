<template>
  <div>
    <div class="d-flex align-center justify-between">
        <h2 class="title">Contact List</h2>
        <div class="button-default" @click="updateShowAdd(true)">Add</div>
    </div>
    <div class="table-container">
        <div class="contact-list-header d-flex align-center justify-between contact-list-wrapper">
            <h4>Name</h4>
            <h4>Actions</h4>
        </div>
        <div class="d-flex align-center justify-between contact-list-wrapper" v-for="contact in contacts" :key="contact.id">
            <h4>{{ contact.name }}</h4>
            <div class="d-flex align-center justify-between gaps-8">
                <div @click="editContact(contact)">
                    <img src="/view.png" alt="view">
                </div>
                <div @click="deleteContact(contact.id)">
                    <img src="/delete.png" alt="delete">
                </div>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["contacts"],
  methods: {
    editContact(contact) {
      this.$emit("edit-contact", contact);
      this.$emit("update-show-detail", true);
    },
    deleteContact(id) {
      this.$emit("delete-contact", id);
    },
    updateShowAdd(value) {
        this.$emit("update-show-add", value);
    },
  },
};
</script>


<style scoped>
.table-container {
    padding: 12px 0;
    border: 1px solid #e3e3e3;
    border-radius: 6px;
}

.contact-list-header {
    border-bottom: 1px solid #e3e3e3;
    padding: 0 24px;
}

.contact-list-wrapper {
    padding: 0 24px;
}

</style>
