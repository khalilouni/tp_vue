<template>
    <div class="container">
      <!-- Section-->
      <section class="py-5">
        <div class="container px-4 px-lg-5 mt-5">
          <div class="row gx-4 gx-lg-5 row-cols-2 row-cols-md-3 row-cols-xl-2 justify-content-center">
            <div class="col-sm-12">
              <h4 class="mb-3">Ajouter un nouveau produit</h4>
              <div class="needs-validation" novalidate>
                <div class="row g-2">
                  <div v-if="!submitted">
                  <div class="col-12">
                    <label for="productName" class="form-label">Nom du produit</label>
                    <input type="text" class="form-control" id="productName" placeholder="" required v-model="product.name"/>
                    <div class="invalid-feedback">Valid name is required.</div>
                  </div>
                  <div class="col-12">
                    <label for="productPhoto" class="form-label">Photo du produit</label>
                    <input type="text" class="form-control" id="productPhoto" placeholder="" required v-model="product.photo"/>
                    <div class="invalid-feedback">
                      Valid photo path is required.
                    </div>
                  </div>
                  <div class="col-12">
                    <label for="productPrice" class="form-label">Prix</label>
                    <div class="input-group has-validation">
                      <span class="input-group-text">CAD</span>
                      <input type="text" class="form-control" id="productPrice" placeholder="" required v-model="product.price"/>
                      <div class="invalid-feedback">Price is required.</div>
                    </div>
                  </div>
                  <div class="col-12">
                    <label for="productDescription" class="form-label">Description du produit</label>
                    <textarea class="form-control" id="productDescription" v-model="product.description"></textarea>
                    <div class="invalid-feedback">Valid description</div>
                  </div>
                  <div class="col-12">
                    <label for="productCategorie" class="form-label">Categorie du produit</label>
                    <input type="text" class="form-control" id="productCategorie" placeholder="" required v-model="product.categorie"/>
                  </div>
                  <button class="w-100 btn btn-secondary btn-lg mt-3" type="button" @click="saveProduct">Save </button>
                  </div>
                  <div v-else>
                    <div  class="alert alert-success alert-dismissible fade show" role="alert">
                    <strong> Votre ajout est un success!</strong>
                    <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
                    </div>
                    <button class="w-100 btn btn-success btn-lg mt-3" type="button" @click="newProduct">Nouveau produit </button>
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
  props: ['addInv'],
  data () {
    return {
      submitted: false,
      product: {
        name: '',
        photo: '',
        price: '',
        description: '',
        categorie: ''
      }
    }
  },
  methods: {
    saveProduct () {
      console.log(this.product)
      ProductDataService.create(this.product)
        .then(response => {
          this.product.id = response.data.id
          this.addInv(this.product)
          this.submitted = true
        })
    },

    newProduct () {
      this.submitted = false
      this.product = {}
    }
  }
}

</script>
