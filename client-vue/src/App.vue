<template>
  <!-- Navigation-->
  <nav className="navbar navbar-expand-lg  bg-dark p-3 mb-2 bg-dark">
      <div className="container-fluid">
          <ul className="navbar-nav me-auto mb-2 mb-lg-0 text-white">
                <li class="nav-item "><router-link class="nav-link active text-white" aria-current="page" to="/">All products</router-link></li>
                <li class="nav-item"><router-link class="nav-link text-white" to="/about">About</router-link></li>
          </ul>
          <button class="btn btn-danger">
            <router-link class="nav-link" to="/add-product">Add product</router-link>
          </button>
      </div>
  </nav>
  <router-view
  :inventory = "inventory"
  :addInv = "addInventory"
  :removeInv = "removeInventory"
  :updateInv = "updateInventory"
  />
</template>

<script>

import ProductDataService from '@/services/ProductDataService'
export default {
  data () {
    return {
      inventory: []
    }
  },
  methods: {
    addInventory (data) {
      this.inventory.push(data)
    },
    removeInventory (index) {
      this.inventory.splice(index, 1)
    },
    updateInventory (index, data) {
      this.inventory[index].name = data.name
      this.inventory[index].photo = data.photo
      this.inventory[index].price = data.price
      this.inventory[index].description = data.description
      this.inventory[index].type = data.type
    }
  },
  mounted () {
    ProductDataService.getAll()
      .then(response => {
        this.inventory = response.data
        console.log(response.data)
      })
  }
}

</script>
