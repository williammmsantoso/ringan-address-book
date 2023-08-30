<template>
  <div id="app">
    <h1 class="text-center">Address Book</h1>
    <ContactForm
      :contact="editingContact"
      @add-contact="addContact"
      @update-contact="updateContact"
      :show-add="showAdd"
      @update-show-add="updateShowAdd"
    />
    <ContactList
      :contacts="contacts"
      @edit-contact="editContact"
      @delete-contact="deleteContact"
      :show-add="showAdd"
      @update-show-add="updateShowAdd"
      @update-show-detail="updateShowDetail"
    />
    <ContactDetail
      :selected-contact="selectedContact"
      @update-contact="updateContact"
      :show-detail="showDetail"
      @update-show-detail="updateShowDetail"
    />
  </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactList from "@/components/ContactList.vue";
import ContactDetail from "@/components/ContactDetail.vue";

export default {
  components: {
    ContactForm,
    ContactList,
    ContactDetail,
  },
  data() {
    return {
      contacts: [],
      editingContact: null,
      selectedContact: null,
      showAdd: false,
      showDetail: false,
    };
  },
  methods: {
    addContact(newContact) {
      newContact.id = Date.now();
      this.contacts.push(newContact);
    },
    editContact(contact) {
      this.editingContact = contact;
      this.selectedContact = contact; // Set selectedContact for ContactDetail
    },
    updateContact(id, updatedContact) {
      const index = this.contacts.findIndex((contact) => contact.id === id);
      if (index !== -1) {
        this.contacts[index] = updatedContact;
        this.editingContact = null;
        this.selectedContact = null;
      }
    },
    deleteContact(id) {
      this.contacts = this.contacts.filter((contact) => contact.id !== id);
      this.selectedContact = null; // Reset selectedContact after deleting
    },
    updateShowAdd(value) {
      this.showAdd = value;
    },
    updateShowDetail(value) {
      this.showDetail = value;
    }
  },
};
</script>

<style>
/* START GLOBAL STYLE */
body, html {
  background-color: #F7F7F9;
  padding: 0 24px;
}

.d-flex {
  display: flex;
  flex-direction: row;
}

.align-center {
  align-items: center;
}

.justify-between {
  justify-content: space-between;
}

.text-center {
  text-align: center;
}

.gaps-8 {
  gap: 8px;
}

/* END GLOBAL STYLE */

/* START BUTTON */

.button-default {
  background-color: #6FA7FE;
  color: #fff;
  padding: 12px 24px;
  border-radius: 6px;
  margin: 16px 0;
  cursor: pointer;
  text-align: center;
}

.button-default.type-red {
  background-color: red;
}

.button-default:hover {
  opacity: 0.8;
}
/* END BUTTON */

/* START INPUT */

.input-wrapper {
    display: flex;
    flex-direction: column;
    margin-bottom: 16px;
}

.input-wrapper label {
    margin-bottom: 8px;
}

input {
  padding: 0 8px;
  border: 1px solid #e3e3e3;
  height: 32px;
  border-radius: 4px;
  font-size: 14px;
}
/* END INPUT */


/* START MODAL */
.popup-dialog-container {
  font-family: "Mulish", sans-serif !important;
  visibility: hidden;
  opacity: 0;
  -webkit-transition: ease-in-out all 0.4s;
  transition: ease-in-out all 0.4s;
}

.popup-dialog-container.show {
  visibility: visible;
  opacity: 1;
  -webkit-transition: ease-in-out all 0.4s;
  transition: ease-in-out all 0.4s;
}

.popup-dialog-wrapper.show .modal {
  visibility: visible;
  opacity: 1;
  display: block;
  -webkit-transition: ease-in-out all 0.4s;
  transition: ease-in-out all 0.4s;
}

.popup-dialog-wrapper.show .backdrop {
  display: block;
  -webkit-transition: ease-in-out all 0.3s;
  transition: ease-in-out all 0.3s;
  cursor: pointer;
}

.popup-dialog-wrapper .backdrop {
  position: fixed;
  display: none;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
  z-index: 10;
  top: 0;
  left: 0;
  overflow: auto;

  -webkit-transition: ease-in-out all 0.3s;
  transition: ease-in-out all 0.3s;
}

.popup-dialog-wrapper .modal {
  visibility: hidden;
  opacity: 0;
  display: unset;

  position: fixed;
  top: 50%;
  left: 50%;
  width: 40%;

  transform: translate(-50%, -50%);

  height: auto;
  background-color: #fff;
  box-shadow: 0px 0px 40px rgba(40, 40, 40, 0.06);
  border-radius: 8px;

  z-index: 20;
  overflow-y: auto;

  padding: 16px;

  -webkit-transition: ease-in-out all 0.4s;
  transition: ease-in-out all 0.4s;
}

.popup-dialog-wrapper .modal .modal-content .button-close {
  position: absolute;
  right: 0;
  top: 0;
}

.popup-dialog-wrapper .modal .modal-content {
  width: 100%;
  height: auto;
  padding: 16px 0;
  position: relative;
}

/* END MODAL */

@media screen and (max-width: 800px) {
  body, html {
    padding: 6px;
  }

  .popup-dialog-wrapper .modal{
    width: 80%;
  }
}
</style>
