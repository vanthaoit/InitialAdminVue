
<template>
  <section class="content">

    <div class="row center-block">

      <div class="col-md-12">
        <div class="box">
          <div class="box-header">
            <button class="btn btn-success" @click.prevent="$modals.createModal.$show()">Create</button>
          </div>
          <!-- /.box-header -->
          <div class="box-body">
            <div class="dataTables_wrapper form-inline dt-bootstrap" id="example1_wrapper">
              <div class="row">
                <div class="col-sm-6">
                  <div id="example1_length" class="dataTables_length">

                  </div>
                </div>
              </div>

              <div v-if="productResult[0]" class="row">
                <div class="col-sm-12 table-responsive">
                  <table aria-describedby="example1_info" role="grid" id="example1" class="table table-bordered table-striped dataTable">
                    <thead>
                      <tr role="row">
                        <th aria-label="Rendering engine: activate to sort column descending" aria-sort="ascending" style="width: 50px;" colspan="1" rowspan="1" aria-controls="example1" tabindex="0" class="sorting_asc">Id</th>
                        <th aria-label="Rendering engine: activate to sort column descending" aria-sort="ascending" style="width: 167px;" colspan="1" rowspan="1" aria-controls="example1" tabindex="0" class="sorting_asc">Name</th>
                        <th aria-label="Browser: activate to sort column ascending" style="width: 207px;" colspan="1" rowspan="1" aria-controls="example1" tabindex="0" class="sorting">Content</th>
                        <th aria-label="Platform(s): activate to sort column ascending" style="width: 182px;" colspan="1" rowspan="1" aria-controls="example1" tabindex="0" class="sorting">Description</th>
                        <th aria-label="Engine version: activate to sort column ascending" style="width: 142px;" colspan="1" rowspan="1" aria-controls="example1" tabindex="0" class="sorting">Price</th>
                        <th aria-label="CSS grade: activate to sort column ascending" style="width: 101px;" colspan="1" rowspan="1" aria-controls="example1" tabindex="0" class="sorting">Date Modified</th>
                      </tr>
                    </thead>
                    <tbody>
                      <tr v-for="item in productResult" :key="item.id" class="odd" role="row">
                        <td>{{item.Id}}</td>
                        <td class="sorting_1">{{item.Name}}</td>
                        <td class="max-character-length">{{item.Content}}</td>
                        <td class="max-character-length">{{item.Description}}</td>
                        <td>{{item.Price}}</td>
                        <td>{{item.DateModified | formatDate}}</td>
                      </tr>
                    </tbody>
                    <tfoot>
                      <tr>
                        <th colspan="1" rowspan="1">Id</th>
                        <th colspan="1" rowspan="1">Name</th>
                        <th colspan="1" rowspan="1">Content</th>
                        <th colspan="1" rowspan="1">Description</th>
                        <th colspan="1" rowspan="1">Price</th>
                        <th colspan="1" rowspan="1">Date Modified</th>
                      </tr>
                    </tfoot>
                  </table>
                  
                </div>
              </div>
            </div>
            <!-- /.box-body -->
          </div>
        </div>
      </div>
        
          <vudal name="createModal">
          <form @submit.prevent="createProduct" class="product-form">
            <div class="header center header-product">
              Create Product
            </div>
            <div class="scrollbar" id="content-product-cover">

              <div class="content row row-product force-overflow form-group">
              <div class="col-sm-3 label-product">Name (*)</div>
              <div class="col-sm-9">
                <input type="text" class="content-product form-control" required v-model="products.Name"/>
              </div>
              
              </div>
              <div class="content row row-product force-overflow">
                <div class="col-sm-3 label-product">Category</div>
                <div class="col-sm-9">
                  <select v-if="categoryList[0]" v-model="categorySelected" class="selected-option">
                    <option v-for="item in categoryList" :key="item.Id" v-bind:value="item.Id">{{item.Name}}</option>
                  </select>
                </div>
                
              </div>
              <div class="content row row-product force-overflow">
                <div class="col-sm-3 label-product">Price</div>
                <div class="col-sm-9">
                  <input type="text" class="content-product" v-model="products.Price"/>
                </div>
                
              </div>
              <div class="content row row-product force-overflow">
                <div class="col-sm-3 label-product">Promotion Price</div>
                <div class="col-sm-9">
                  <input type="text" class="content-product" value="" v-model="products.PromotionPrice"/>
                </div>
                
              </div>
              <div class="content row row-product force-overflow">
                <div class="col-sm-3 label-product">Original Price</div>
                <div class="col-sm-9">
                  <input type="text" class="content-product" v-model="products.OriginalPrice"/>
                </div>
                
              </div>
              <div class="content row row-product force-overflow">
                <div class="col-sm-3 label-product">Content (*)</div>
                <div class="col-sm-9">
                  <textarea type="text" class="content-product form-control" required  aria-valuemax="" v-model="products.Content"></textarea>
                </div>
                
              </div>
              <div class="content row row-product force-overflow">
                <div class="col-sm-3 label-product">Description (*)</div>
                <div class="col-sm-9">
                  <textarea type="text" class="content-product form-control" required v-model="products.Description"></textarea>
                </div>
                
              </div>
              <div class="content row row-product force-overflow form-group">
              <div class="col-sm-3 label-product">Tags (*)</div>
              <div class="col-sm-9">
                <input type="text" class="content-product form-control" required v-model="products.Tags"/>
              </div>
              </div>
              <div class="content row row-product force-overflow">
                <div class="col-sm-3 label-product">Home Flag</div>
                <div class="col-sm-9">
                  <input v-model="checkHomeFlag" type="radio" name="homeFlag" value="true"> True<br>
                  <input v-model="checkHomeFlag" type="radio" name="homeFlag" value="false"> False<br>
                </div>
                
              </div>
              <div class="content row row-product force-overflow">
                <div class="col-sm-3 label-product">Hot Flag</div>
                <div class="col-sm-9">
                  <input v-model="checkHotFlag" type="radio" name="hotFlag" value="true"> True<br>
                  <input v-model="checkHotFlag" type="radio" name="hotFlag" value="false"> False<br>
                </div>
                
              </div>
              <div class="content row row-product force-overflow">
                <div class="col-sm-3 label-product">View count</div>
                <div class="col-sm-9">
                  <input type="text" class="content-product" v-model="products.ViewCount"/>
                </div>
                
              </div>
              <div class="content row row-product force-overflow">
                <div class="col-sm-3 label-product">Seo Description (*)</div>
                <div class="col-sm-9">
                  <textarea type="text" class="content-product form-control" required value="" v-model="products.SeoDescription"></textarea>
                </div>
                
              </div>
              <div class="content row row-product force-overflow">
                <div class="col-sm-3 label-product">Status</div>
                <div class="col-sm-9">
                  <select v-model="selected" class="selected-option">
                    <option value="InActive">InActive</option>
                    <option value="Active">Active</option>
                  </select>
                </div>
                
              </div>
            </div>
            
            <div class="actions product-form-action">
              <button type="submit" class="button-min-width btn btn-primary">OK</button>
              <div class="cancel btn btn-danger">Close</div>
            </div>
          </form>
          </vudal>
        
    </div>
    

  </section>
</template>

<script>
import $ from "jquery";
import { HttpGet, HttpPost } from "../../api/index.js";
import Vudal from "../../store/utilities/index.js";
import Vue from "vue";

import {
  HTTPS_CONSTANTS,
  GENERAL_CONSTANTS
} from "../../config/http.constants.js";

// Require needed datatables modules
require("datatables.net");
require("datatables.net-bs");
const moment = require("moment");
require("moment/locale/es");

Vue.use(require("vue-moment"), {
  moment
});

export default {
  name: "Products",
  components: { Vudal },
  data() {
    return {
      productResult: [],
      categoryList: [],
      products: {},
      nameProduct: "",
      error: null,
      categorySelected: 1,
      checkHomeFlag: true,
      checkHotFlag: true,
      selected: "InActive"
    };
  },
  created: function() {},
  methods: {
    callProducts() {
      let uri = GENERAL_CONSTANTS.PRODUCT + "/" + GENERAL_CONSTANTS.GET_ALL;

      HttpGet(uri)
        .then(response => {
          if (response.status !== 200) {
            this.error = response.statusText;
            return;
          }
          this.productResult = response.data;
        })
        .catch(e => {
          this.error = e.response.statusText;
        });
    },
    createProduct() {
      let uri = GENERAL_CONSTANTS.PRODUCT + "/" + HTTPS_CONSTANTS.POST;
      this.products.CategoryId = this.categorySelected;
      if (this.products.Price == undefined) this.products.Price = 1;
      if (this.products.PromotionPrice == undefined)
        this.products.PromotionPrice = 1;
      if (this.products.OriginalPrice == undefined)
        this.products.OriginalPrice = 1;
      if (this.products.Name == undefined) this.products.Name = "";
      if (this.products.Content == undefined) this.products.Content = "";
      if (this.products.Description == undefined)
        this.products.Description = "";
      this.products.HomeFlag = this.checkHomeFlag;
      this.products.HotFlag = this.checkHotFlag;
      if (this.products.ViewCount == undefined)
        this.products.ViewCount = 1;
      
      if (this.products.SeoDescription == undefined)
        this.products.SeoDescription = "";
      this.products.DateCreated = new Date();
      this.products.DateModified = new Date();
      this.products.Image = "";
      if (this.products.Tags == undefined) this.products.Tags = "";
      this.products.Unit = "";
      this.products.SeoPageTitle = "";
      this.products.SeoKeywords = "";
      this.products.Status = this.selected;
      HttpPost(uri, this.products)
        .then(response => {
          this.productResult = response.data;
          if (this.productResult != undefined) {
            this.$notify({
              group: "foo",
              title:
                "<h4 style='text-align:center'>successful create product</h4>",
              text:
                "<h3 style='text-align:center'>You create successfully " +
                " with Id = " +
                this.productResult.Id +
                "</h3>",
              type: "success",
              duration: 2000,
              speed: 2000,
              data: {}
            });
          }
          setTimeout(() => {
            window.location.href =
              "http://192.168.206.43:8000/administrator/products";
          }, 1500);
        })
        .catch(e => {
          this.error = e.response.statusText;
        });
    },
    getCategory() {
      let uri =
        GENERAL_CONSTANTS.PRODUCT_CATEGORY + "/" + GENERAL_CONSTANTS.GET_ALL;
      HttpGet(uri)
        .then(response => {
          this.categoryList = response.data;
        })
        .catch(e => {
          this.error = e.response.statusText;
        });
    }
  },
  mounted() {
    this.callProducts();
    this.getCategory();
  },
  updated() {
    this.$nextTick(() => {
      $("#example1").DataTable();
    });
  }
};
</script>


<style>
@import url("/static/js/plugins/datatables/dataTables.bootstrap.css");
table.dataTable thead .sorting:after,
table.dataTable thead .sorting_asc:after,
table.dataTable thead .sorting_desc:after {
  font-family: "FontAwesome";
}

table.dataTable thead .sorting:after {
  content: "\f0dc";
}

table.dataTable thead .sorting_asc:after {
  content: "\f0dd";
}

table.dataTable thead .sorting_desc:after {
  content: "\f0de";
}
.max-character-length {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 200px;
}
</style>
