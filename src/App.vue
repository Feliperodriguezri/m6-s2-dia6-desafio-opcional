<template>
  <div id="app" class="py-5">
    <header>
      <main class="container">
        <h1 class="text-center">Iniciando Proyecto</h1>
        <section class="row justify-content-center">
          <!-- los data son atributos personalizados para que pueda asignar ciertos valores al elemento que despues pueda utilizar -->

          <!-- usamos v-for para crear de forma dinamica tantas card como productos tenga -->
          <div class="col-12 col-md-6 col-lg-4 " v-for="producto in productos" :key="producto.id">
            <div class="card" style="width: 18rem">
              <img :src="producto.pathImg" class="card-img-top" :alt="producto.nombre" />
              <div class="card-body">
                <h5 class="card-title">{{ producto.nombre }}</h5>
                <p class="card-text">
                  {{ producto.descripcionCorta }}
                </p>
                <div>
                  <button class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#miModal" :data-producto-id= "producto.id"
                    @click="mostrar">
                    Ver detalles
                  </button>
                </div>
              </div>
            </div>
          </div>
        </section>


      </main>
    </header>
    
    <!-- Modal -->
    <div class="modal fade" id="miModal" tabindex="-1" aria-labelledby="miModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="miModalLabel">{{ currentProducto.nombre }}</h1>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <img :src="currentProducto.pathImg" :alt="currentProducto.nombre">
            <p><span>Descripcion: </span>{{ currentProducto.descripcionLarga }}</p>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary">Save changes</button>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      productos: [
        { id: 1, nombre: "Producto 1", descripcionCorta: "descripcion 1", pathImg: "./img/zapatilla1.jpg", descripcionLarga: "zapatillas modelo x marca x" },
        { id: 2, nombre: "Producto 2", descripcionCorta: "descripcion 2", pathImg: "./img/zapatilla2.jpg", descripcionLarga: "zapatillas modelo y marca y" },
        { id: 2, nombre: "Producto 2", descripcionCorta: "descripcion 2", pathImg: "./img/zapatilla3.jpg", descripcionLarga: "zapatillas modelo z marca z" },
      ],
      currentProducto: {}
    }
  },
  methods: {
    mostrar: function (event) {
      let element = event.target;
      let productoId = element.dataset.productoId;

      //buscar elemento dentro del array de producto
      let foundProducto = this.productos.find(producto => producto.id == productoId);
      if (foundProducto) {
        this.currentProducto = foundProducto;
        console.log(foundProducto)
      } else {
        alert("Producto no encontrado");
      }
    }
  }
};
</script>

<style></style>
