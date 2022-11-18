<template>
    <div class="product-add">
      <!-- Section-->
      <section class="py-5">
        <div class="container px-4 px-lg-5 mt-5">
          <div class="row gx-4 gx-lg-5 row-cols-2 row-cols-md-3 row-cols-xl-2 justify-content-center">
            <div class="col-sm-12">
              <h4 class="mb-3">Modifier produit</h4>
              <div class="needs-validation" novalidate>
                <div class="row g-2">
                  <div class="col-12">
                    <label for="productName" class="form-label">Nom du produit</label>
                    <input type="text" class="form-control" id="productName" placeholder="" name="name" v-model="product.name" required/>
                    <div class="invalid-feedback">Valid name is required.</div>
                  </div>
                  <div class="col-12">
                    <label for="productPhoto" class="form-label">Photo du produit</label>
                    <input type="text" class="form-control" id="productPhoto" placeholder="" name="photo" v-model="product.photo" required/>
                    <div class="invalid-feedback">
                      Valid photo path is required.
                    </div>
                  </div>
                  <div class="col-12">
                    <label for="productPrice" class="form-label">Prix</label>
                    <div class="input-group has-validation">
                      <span class="input-group-text">CAD</span>
                      <input type="text" class="form-control" id="productPrice" placeholder="" name="price" v-model="product.price" required/>
                      <div class="invalid-feedback">Price is required.</div>
                    </div>
                  </div>
                  <div class="col-12">
                    <label for="productDescription" class="form-label">Description du produit</label>
                    <textarea class="form-control" id="productDescription" placeholder="" name="description" v-model="product.description"></textarea>
                    <div class="invalid-feedback">Valid description</div>
                  </div>
                  <div class="col-12">
                    <label for="productCategorie" class="form-label">Categorie du produit</label>
                    <input type="text" class="form-control" id="productCategorie" placeholder="" required v-model="product.categorie"/>
                  </div>
                  <button class="w-100 btn btn-secondary btn-lg mt-3" type="button" @click="updateProduct" >update </button>
                  <div>
                    <div  class="alert alert-success alert-dismissible fade show" role="alert" v-if="submitted">
                    <strong> Votre mise a jour est un success!</strong>
                    <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
                    </div>
                    <button class="w-100 btn btn-danger btn-lg mt-3" type="button" @click="deleteProduct">Delete </button>
                  </div>
                  <hr class="my-4">
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
  </template>

<script>
import ProductDataService from '@/services/ProductDataService'

export default {
  props: ['removeInv', 'inventory', 'updateInv', 'remove'],
  data () {
    return {
      submitted: false,
      product: {},
      id: parseInt(this.$route.params.id)
    }
  },
  methods: {
    updateProduct () {
      ProductDataService.update(this.id, this.product)
        .then(response => {
          this.updateInv(this.productIndex, this.product)
          this.submitted = true
        })
    },
    deleteProduct () {
      ProductDataService.delete(this.id)
        .then(response => {
          this.removeInv(this.productIndex)
          this.$router.push({ name: 'home' })
        })
    }
  },
  computed: {
    productIndex () {
      const index = this.inventory.findIndex((p) => {
        return p.id === this.id
      })
      return index
    }
  },
  mounted () {
    ProductDataService.get(this.id)
      .then(response => {
        this.product = response.data
      })
  }
}
</script>
