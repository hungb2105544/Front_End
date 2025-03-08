<template>
  <div class="page">
    <h4>Thêm Liên hệ</h4>
    <ContactForm
      :contact="newContact"
      @submit:contact="createContact"
      @delete:contact="deleteContact"
    />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
  components: {
    ContactForm,
  },
  data() {
    return {
      newContact: {
        name: "",
        email: "",
        address: "",
        phone: "",
        favorite: false,
      },
      message: "",
    };
  },
  methods: {
    async createContact(data) {
      try {
        await ContactService.create(data);
        alert("Liên hệ được tạo thành công.");
        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.error("Lỗi khi tạo liên hệ:", error);
        this.message = "Có lỗi xảy ra khi tạo liên hệ.";
      }
    },
    deleteContact() {
      // Không cần xóa khi thêm mới, chỉ cần reset form
      this.newContact = {
        name: "",
        email: "",
        address: "",
        phone: "",
        favorite: false,
      };
      this.message = "Hành động xóa đã bị hủy vì đang thêm mới.";
    },
  },
  created() {
    // Reset form khi component được tạo
    this.newContact = {
      name: "",
      email: "",
      address: "",
      phone: "",
      favorite: false,
    };
  },
};
</script>

<style scoped>
.page {
  max-width: 400px;
  margin: auto;
}
</style>
