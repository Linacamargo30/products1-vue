<template>
  <div class="row mt-3">
    <div class="col-md-6 offset-md-3">
      <div class="card">
        <div class="card-header bg-dark text-white text-center">
          Editar Producto
        </div>
        <div class="card-body">
          <form v-on:submit="guardar">
            <div class="input-group mb-3">
              <span class="input-group-text"
                ><i class="fa-solid fa-gift"></i
              ></span>
              <input
                type="text"
                v-model="name"
                id="nombre"
                class="form-control"
                maxlength="50"
                placeholder="Nombre"
                required
              />
            </div>
            <div class="input-group mb-3">
              <span class="input-group-text"
                ><i class="fa-solid fa-gift"></i
              ></span>
              <input
                type="text"
                v-model="tipo document"
                id=" tipo doc"
                class="form-control"
                placeholder="Tipo doc"
                step="0.01"
                required
              />
            
            <div class="input-group mb-3">
              <span class="input-group-text"
                ><i class="fa-solid fa-dollar-sign"></i
              ></span>
              <input
                type="number"
                v-model="document"
                id="documento"
                class="form-control"
                maxlength="150"
                placeholder="Documento"
                required
              />
            </div>
              <div class="input-group mb-3">
              <span class="input-group-text"
                ><i class="fa-solid fa-dollar-sign"></i
              ></span>
              <input
                type="email"
                v-model="email"
                id="correo"
                class="form-control"
                placeholder="Correo"
                step="0.01"
                required
              />
            </div>
             <div class="input-group mb-3">
              <span class="input-group-text"
                ><i class="fa-solid fa-dollar-sign"></i
              ></span>
              <input
                type="number"
                v-model="phone"
                id="telefono"
                class="form-control"
                placeholder="Telefono"
                step="0.01"
                required
              />
            </div>
            <div class="input-group mb-3">
              <span class="input-group-text"
                ><i class="fa-solid fa-gift"></i
              ></span>
              <input
                type="text"
                v-model="direction"
                id="direccion"
                class="form-control"
                placeholder="Direccion"
                step="0.01"
                required
              />
            </div>
            <div class="input-group mb-3">
              <span class="input-group-text"
                ><i class="fa-solid fa-gift"></i
              ></span>
              <input
                type="text"
                v-model="city"
                id="ciudad"
                class="form-control"
                placeholder="Ciudad"
                step="0.01"
                required
              />
            </div>
            <div class="d-grid col-6 mx-auto">
              <button class="btn btn-success">
                <i class="fa-solid fa-floppy-disk"></i>Guardar
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { show_alerta, enviarSolicitud } from "../funciones";
import { useRoute } from "vue-router";
import axios from "axios";
export default {
  data() {
    return {
      id: 0,
      name: "",
      description: "",
      price: "",
      url: "http://laraproducts.run/api/products",
    };
  },
  mounted() {
    const route = useRoute();
    this.id = route.params.id;
    this.getProduc();
    this.url = url + "/" + this.id;
  },
  methods: {
    getProduc() {
      axios
        .get(this.url)
        .then(
          (response) => (
            (this.name = response.data["name"]),
            (this.description = response.data["description"]),
            (this.price = response.data["price"])
          )
        );
    },
    guardar() {
      event.preventDefault();
      if (this.name.trim() === "") {
        show_alerta("escribe el nombre", "warning", "nombre");
      } else if (this.description.trim() === "") {
        show_alerta("escribe la descripcion ", "warning", "descripcion");
      } else if (this.price.trim() === "") {
        show_alerta("escribe el precio ", "warning", "precio");
      } else {
        var parametros = {
          name: this.name.trim(),
          description: this.description.trim(),
          price: this.price,
        };
        enviarSolicitud("POST", parametros, this.url, "Producto actualizado");
      }
    },
  },
};
</script>
