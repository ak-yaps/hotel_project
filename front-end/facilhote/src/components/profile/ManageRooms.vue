<template>
  <div class="tab-pane table-responsive" id="rooms">
    <h4 class="my-2">Liste des chambres</h4>
    <table v-if="$store.state.users.user.is_admin" class="table table-hover table-striped">
      <thead>
        <tr>
          <th scope="col">Numéro de chambre</th>
          <th scope="col">État de la chambre</th>
          <th scope="col">Type de chambre</th>
          <th scope="col">Couleur associée</th>
          <th colspan="2">
            <button type="button" class="btn btn-success">
              <font-awesome-icon icon="plus-circle" size="lg"/>
            </button>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="room in roomsData" :key="room.id_room">
          <th scope="row" :contenteditable="editMode">{{ room.room_nb }}</th>
          <td :contenteditable="editMode">{{ room.room_status }}</td>
          <td :contenteditable="editMode">{{ room.room_type }}</td>
          <td :contenteditable="editMode">{{ room.color }}</td>
          <td>
            <button type="button" @click="editRoom(room)" class="btn btn-info">
              <font-awesome-icon icon="edit" size="lg"/>
            </button>
          </td>
          <td>
            <button type="button" @click="deleteRoom(room)" class="btn btn-danger">
              <font-awesome-icon icon="trash-alt" size="lg"/>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    <div v-else class="alert alert-info">
      <h4 class="alert-heading">Attention!</h4>
      <p
        class="mb-0"
      >Vous n'avez pas les droits nécessaires pour effectuer cette opération, veuillez contacter votre administrateur.</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      editMode: false
    };
  },
  methods: {
    editRoom(room) {
      console.log(index);
      this.editMode = true;
    },
    deleteRoom(room) {
      let answer = confirm(
        `Étes-vous sûr de vouloir supprimer la chambre numéro ${room.room_nb} ?`
      );
      if (answer) {
        console.log(room);
        // this.$store.dispatch("rooms/deleteRoom");
      }
    }
  },
  computed: {
    roomsData() {
      return this.$store.getters["rooms/roomsData"];
    }
  },
  created() {
    this.$store.dispatch("rooms/getRoomsData");
  }
};
</script>

<style scoped>
.input-bg {
  background: #fff;
}
</style>


