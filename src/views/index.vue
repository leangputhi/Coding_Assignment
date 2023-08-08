<template>
    <!-- overlay -->
    <div class="pt-20">
          <!-- search and filter -->
          <div class="flex justify-between my-4 mx-10">
              <div class="">
                <input
                type="text"
                placeholder="Search Country here..."
                v-model="search"
                class="border  py-3.5 text-lg  rounded-lg  pl-3 text-gray-700 bg-white border-gray-500 border rounded-md  dark:border-yellow-600 dark:placeholder-yellow-400 focus:border-yellow-400 dark:focus:border-yellow-300 focus:ring-yellow-40 focus:outline-none focus:ring focus:ring-yellow-300"
                />
                <svg
                class="w-5 cursor-pointer absolute top-0 right-2 mt-4 mr-5"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 512 512"
                fill="#ddd"
                >
                <path
                    d="M500.3 443.7l-119.7-119.7c27.22-40.41 40.65-90.9 33.46-144.7C401.8 87.79 326.8 13.32 235.2 1.723C99.01-15.51-15.51 99.01 1.724 235.2c11.6 91.64 86.08 166.7 177.6 178.9c53.8 7.189 104.3-6.236 144.7-33.46l119.7 119.7c15.62 15.62 40.95 15.62 56.57 0C515.9 484.7 515.9 459.3 500.3 443.7zM79.1 208c0-70.58 57.42-128 128-128s128 57.42 128 128c0 70.58-57.42 128-128 128S79.1 278.6 79.1 208z"
                />
                </svg>                                
              </div>

              <!-- pagination -->

              <div class="flex items-center justify-center mt-4">
                <nav class="flex font-semibold items-center">
                  <a
                    href="#"
                    class="px-3   py-2 mr-2 rounded-md bg-gray-200 text-gray-700 hover:bg-gray-300 transition ease-in-out delay-100  duration-300"
                    
                    @click="prevPage"
                  >
                    Previous
                  </a>
                  <a
                    href="#"
                    class="px-3 py-2 mr-2 rounded-md bg-gray-200 text-gray-700 hover:bg-gray-300"
                  >
                    {{ currentPage }} of {{ totalPages }}
                  </a>

                  <a
                    href="#"
                    class="px-6 py-2 mr-2 rounded-md bg-gray-200 text-gray-700 hover:bg-gray-300 transition ease-in-out delay-100  duration-300"
                    @click="nextPage"
                  >
                  Next
                  </a>
                  <!-- Add more pagination links as needed -->
                </nav>
              </div>


              <div class="">
                <button @click="showcate =! showcate" class="relative py-1 w-64 flex  items-center bg-white border focus:outline-none shadow text-gray-600
                rounded focus:ring ring-gray-200 group">
                        <span class="p-3.5">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M9.568 3H5.25A2.25 2.25 0 003 5.25v4.318c0 .597.237 1.17.659 1.591l9.581 9.581c.699.699 1.78.872 2.607.33a18.095 18.095 0 005.223-5.223c.542-.827.369-1.908-.33-2.607L11.16 3.66A2.25 2.25 0 009.568 3z" />
                            <path stroke-linecap="round" stroke-linejoin="round" d="M6 6h.008v.008H6V6z" />
                            </svg>

                        </span>
                        <p class="">{{Selected_Filter}}</p>
                </button>
                <button v-show="showcate" @click="showcate = false" class="fixed inset-0"></button>
                <div v-show="showcate" class="absolute rigth-0 bg-white shadow-md mt-2 rounded w-1/6" style="z-index: 900;">
                    <ul class="grid  grid-cols-1 text-left  border-2 rounded overflow-y-auto " >
                        <li @click="sortByCountryName('asc','ASC (A-Z) ▲')"  class="px-4 py-3 hover:bg-gray-200 ">ASC (A-Z) ▲</li>
                        <li @click="sortByCountryName('desc','DESC (Z-A) ▼')" class="px-4 py-3 hover:bg-gray-200">DESC (Z-A) ▼</li>
                    </ul>
                </div>
              </div>

          </div>
          <!--end search and filter -->

          <!-- Table -->
          <table class=" text-sm text-left text-gray-500 dark:text-gray-400">
            <thead class="text-md font-semibold text-gray-600 uppercase bg-gray-200 dark:bg-gray-700 dark:text-gray-400">
              <tr>
                
                <th scope="col" class="py-3 px-6">Image</th>
                <th scope="col" class="py-3 px-6"> Country Name</th>
                <th scope="col" class="py-3 px-6" >2 character Country Code</th>
                <th scope="col" class="py-3 px-6">3 character Country Code</th>
                <th scope="col" class="py-3 px-6">Native Country Name</th>
                <th scope="col" class="py-3 px-6">Alternative Country Name</th>
                <th scope="col" class="py-3 px-6">Country Calling Codes</th>
              </tr>
            </thead>
            <tbody>
                  <tr v-for="(item, index) in paginatedCountries" :key="index" class="border-b-2 font-semibold">
                    <td  class="py-1 px-6">
                      <img :src="item.flags.png" :alt="item.name.official" class="w-64 h-auto shadow" />
                    </td>
                    <td class="py-1 px-6">
                         <button v-on:click="show_model(item)"> {{ item.name.common }}</button>
                    </td> 
                    <td class="py-1 px-6">{{ item.cca2 }}</td>
                    <td class="py-1 px-6">{{ item.cca3 }}</td>
                    <td class="py-1 px-6"><pre>{{ JSON.stringify(item.name.nativeName, null, 2) }}</pre></td>
                    <td class="py-1 px-6">{{ Object.values(item.altSpellings).join(', ') }}</td>
                    <td class="py-1 px-6"><pre>{{ JSON.stringify(item.idd, null, 2) }}</pre></td>
                  </tr>
            </tbody>
          </table>
           <!-- End Table -->

          <!-- popup model -->
          <div
            v-show="showmodel"
          
            class="fixed inset-0 h-screen w-full flex   justify-center items-start md:items-center pt-10 md:pt-0"
            style=""
          >
              <div v-if="items" class="py-10 bg-white border-2 px-10 shadow-lg rounded-lg w-1/2">
                <div  >
                 
                 <div class="">
                 <p>Flag: <br> <img :src="items.flags.png" :alt="items.name.common" /></p>
                 <p>CCN3: {{ items.cca3 }}</p>
                 <p>Region: {{ items.region }}</p>
                 <p>Subregion: {{ items.subregion }}</p>
                 <p>Languages: {{ Object.values(items.languages).join(', ') }}</p>
                 <p>Currencies: {{ Object.keys(items.currencies).join(', ') }}</p>
                 <p>Translations: {{ Object.keys(items.translations).join(', ') }}</p>
                 <p v-if="items.borders && items.borders.length > 0">Borders: {{ items.borders.join(', ') }}</p>
                 <p v-else>No bordering countries</p>
                 <p>Timezones: {{ items.timezones.join(', ') }}</p>
                 </div>
                 <button v-on:click="showmodel = false" class="px-4 py-2 bg-blue-400 rounded-lg text-white mt-3 ">Close</button>
                </div>    
              </div>

          </div>
          <!-- End popup model -->
          <!-- End Table -->
    </div>

</template>

<script>
import axios from 'axios';
import fuzzysort from 'fuzzysort';


export default {
  data() {
    return {
      search: '',
      Selected_Filter:'ASC (A-Z) ▲', 
      tableLoading: true,
      showmodel: false,
      showcate:false,
      countries: [],
      items:null,
      currentPage: 1,
      itemsPerPage: 25,
      sortOrder: 'asc', // Default sorting order
    };
  },
  created() {
    this.getAllCountries();

  },
  computed: {
    Countries_filter() {
      if (!this.search) return this.countries;

      return fuzzysort.go(this.search, this.countries, {
        key: 'name.common',
      }).map((result) => result.obj);
    },
    Countries_sorted() {
      return this.Countries_filter.slice().sort((a, b) => {
        const nameA = a.name.common.toLowerCase();
        const nameB = b.name.common.toLowerCase();
        return this.sortOrder === 'asc' ? nameA.localeCompare(nameB) : nameB.localeCompare(nameA);
      });
    },
    totalPages() {
      return Math.ceil(this.Countries_sorted.length / this.itemsPerPage);
    },
    paginatedCountries() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.Countries_sorted.slice(startIndex, endIndex);
    },
  },
  methods: {
    async getAllCountries() {
      try {
        const res = await axios.get('https://restcountries.com/v3.1/all');
        this.countries = res.data;

        console.log(this.countries)
 
      } catch (err) {
        console.log(err);
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage -= 1;
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage += 1;
      }
    },
    sortByCountryName(order, name) {
      this.sortOrder = order
      this.Selected_Filter = name

      this.showcate = false
    },

    show_model(item){
        this.items = item
        this.showmodel =! this.showmodel
        console.log(this.showmodel)
        console.log(this.items)
    }
  },
};
</script>

<style>
.bd1 {
  background-color: rgb(0, 183, 255);
  color: white;
}
.bd1:hover {
  background-color: rgb(95, 209, 254);
}
.bg10 {
  background-image: url("../assets/background.png");
  background-size: cover;
}
.bd2 {
  background-image: linear-gradient(to top, #cfd9df 0%, #e2ebf0 100%);
}
</style>
