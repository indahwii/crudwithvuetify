<template>
    <div id="app">
        <center> <h1 style="color: lightblue;"> Simple TodoList App </h1> </center>
        <v-form class="form">
            <v-text-field
            label="Nama Tugas"
            v-model="nama"
            required
            ></v-text-field>

            <v-text-field
            label="Deskripsi"
            v-model="desk"
            required
            ></v-text-field>

            <v-btn @click="addDo" color="#55B359"> Send </v-btn>
            <v-btn @click="clear" color="#FF6666">Delete</v-btn>
        </v-form>

         <v-data-table
            :headers="headers"
            :items="todos"
            hide-actions
            class="elevation-1"
          >
          <template slot="items" slot-scope="props">
              <td class="text-xs-left">{{ props.item.nama }}</td>
              <td class="text-xs-left">{{ props.item.desk }}</td>
              <td class="text-xs-left"> 
                <v-btn icon @click="removeTodo(props.item)">
                  <v-icon color="pink">delete</v-icon>
                </v-btn>    
              </td>
           </template>
        </v-data-table>

    </div>
</template>

<script>
export default {
  data: () => ({
    headers: [
      { text: "Nama Tugas", value: "nama" },
      { text: "Deskripsi", value: "desk" },
      { text: "Hapus", value: "" }
    ],
    nama: "",
    desk: "",
    todos: []
  }),
  methods: {
    addDo() {
      if (this.nama.trim() === "" && this.desk.trim() === "") {
        alert("Data tidak boleh kosong!");
      } else {
        this.todos.push({
          nama: this.nama,
          desk: this.desk
        });
        this.nama = "";
        this.desk = "";
      }
    },
    removeTodo(id) {
      this.todos.splice(id, 1);
    },
    clear() {
      this.nama = "";
      this.desk = "";
    }
  }
};
</script>

<style scoped>
#app {
  margin-top: 30px;
}
.form {
  margin-top: 20px;
  margin-bottom: 50px;
}
</style>