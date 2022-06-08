<template>
	<div class="grid">
		<div class="col-12">
			<div class="card">
				<h5>BANDEJA PROPUESTA DE DISEÑO</h5>
                <br><br>
                <div class="p-fluid grid formgrid">
					<div class="field col-12 mb-2 md:col-8 lg:mb-0">
						<span class="p-input-icon-right p-float-label">
							<InputText type="text" />
                            <label for="dropdown">Busqueda por ID</label>
							<i class="pi pi-search" />
						</span>
					</div>
				</div>
                <br><br>
                <div class="p-fluid grid formgrid">
					<div class="field col-12 mb-2 md:col-4 lg:mb-0">
                        <span class="p-float-label">
						<Calendar id="calendar" :showIcon="true" :showButtonBar="true" v-model="calendarValue"></Calendar>
                        <label for="calendar">Expediente recibido:</label>
                        </span>
					</div>
                    <div class="field col-12 mb-2 md:col-4 lg:mb-0">
						<span class="p-float-label">
                            <Dropdown id="dropdown" :options="cities" v-model="value8" optionLabel="name"></Dropdown>
                            <label for="dropdown">Tipo Vehículo</label>
                        </span>
					</div>
                    <div class="field col-12 mb-2 md:col-4 lg:mb-0">
						<span class="p-float-label">
                            <Dropdown id="dropdown" :options="cities" v-model="value8" optionLabel="name"></Dropdown>
                            <label for="dropdown">Trámite</label>
                        </span>
					</div>
				</div>
                <br><br>
                <div class="p-fluid grid">
					<div class="col-12 mb-2 md:col-6 lg:mb-0" style="padding:0;">
                        <Button label="Solicitudes Nuevas" class="mb-2 p-button-outlined" style="border-radius: 0px;"></Button>
					</div>
                    <div class="col-12 mb-2 md:col-6 lg:mb-0" style="padding:0;">
                        <Button label="Solicitudes con Incidencias" class="mb-2 p-button-outlined" style="border-radius: 0px;"></Button>
					</div>
				</div>
                <br><br>
                <div class="grid">
					<div class="col-12 ">
                        <div class="card">

                             <ul>
                                <li v-for="(user, index) in users" v-bind:key="index">Usuario: {{user.name}}</li>
                               
                            </ul>
                         
                            <h5>Datos J&J </h5>
                            
                            <DataTable :value="usuarios" stripedRows responsiveLayout="scroll" :paginator="true" :rows="10">
                                <Column field="id" header="Code"></Column>
                                <Column field="name" header="Name"></Column>
                              <!--   <Column field="category" header="Category"></Column>
                                <Column field="quantity" header="Quantity"></Column> -->
                            </DataTable>
                            


                           
                        </div>
                    </div>
				</div>

            </div>
		</div>
	</div>

   
</template>

<script>
	
	export default {
        data() {
            return {
                usuarios: []
            }
        },
        //productService: null,
        created() {
            //this.productService = new ProductService();
        },
        mounted() {
            //this.productService.getProductsSmall().then(data => this.products = data);

            let usuarios = async  function getData(){
               
                    const response = await fetch('https://jsonplaceholder.typicode.com/users')
                    const r_data = await response.json()
                    console.log("r_data",r_data)
                    //r_data.forEach(element => console.log(element.name))
                    return r_data
            }

           usuarios().then(val => this.usuarios = val)
            
        }

        /*
		data() {
			return {
				customer1: null,
				customer2: null,
				customer3: null,
				filters1: null,
				filters2: {},
				loading1: true,
				loading2: true,
				idFrozen: false,
				products: null,
				expandedRows: [],
                users: [],
				statuses: [
					'unqualified', 'qualified', 'new', 'negotiation', 'renewal', 'proposal'
				],
				representatives: [
					{name: "Amy Elsner", image: 'amyelsner.png'},
					{name: "Anna Fali", image: 'annafali.png'},
					{name: "Asiya Javayant", image: 'asiyajavayant.png'},
					{name: "Bernardo Dominic", image: 'bernardodominic.png'},
					{name: "Elwin Sharvill", image: 'elwinsharvill.png'},
					{name: "Ioni Bowcher", image: 'ionibowcher.png'},
					{name: "Ivan Magalhaes",image: 'ivanmagalhaes.png'},
					{name: "Onyama Limba", image: 'onyamalimba.png'},
					{name: "Stephen Shaw", image: 'stephenshaw.png'},
					{name: "XuXue Feng", image: 'xuxuefeng.png'}
				],
                
			}
		},
		customerService: null,
		productService: null,
        
		created() {
			this.customerService = new CustomerService();
			this.productService = new ProductService();
			this.initFilters1();

            
		},
      
		mounted() {


			this.productService.getProductsWithOrdersSmall().then(data => this.products = data);
			this.customerService.getCustomersLarge().then(data => {
				this.customer1 = data; 
				this.loading1 = false;
				this.customer1.forEach(customer => customer.date = new Date(customer.date));
			});
			this.customerService.getCustomersLarge().then(data => this.customer2 = data);
			this.customerService.getCustomersMedium().then(data => this.customer3 = data);
			this.loading2 = false;

            let users = async  function getData(){
               
                    const response = await fetch('https://jsonplaceholder.typicode.com/users')
                    const r_data = await response.json()
                    console.log("r_data",r_data)
                    //r_data.forEach(element => console.log(element.name))
                    return r_data
            }


           console.log("data",users().then(val => this.users = val))

            
            
            
		},
		methods: {
			initFilters1() {
				this.filters1 = {
					'global': {value: null, matchMode: FilterMatchMode.CONTAINS},
					'name': {operator: FilterOperator.AND, constraints: [{value: null, matchMode: FilterMatchMode.STARTS_WITH}]},
					'country.name': {operator: FilterOperator.AND, constraints: [{value: null, matchMode: FilterMatchMode.STARTS_WITH}]},
					'representative': {value: null, matchMode: FilterMatchMode.IN},
					'date': {operator: FilterOperator.AND, constraints: [{value: null, matchMode: FilterMatchMode.DATE_IS}]},
					'balance': {operator: FilterOperator.AND, constraints: [{value: null, matchMode: FilterMatchMode.EQUALS}]},
					'status': {operator: FilterOperator.OR, constraints: [{value: null, matchMode: FilterMatchMode.EQUALS}]},
					'activity': {value: null, matchMode: FilterMatchMode.BETWEEN},
					'verified': {value: null, matchMode: FilterMatchMode.EQUALS}
				}
			},
			clearFilter1() {
				this.initFilters1();
			},
			expandAll() {
				this.expandedRows = this.products.filter(p => p.id);
			},
			collapseAll() {
				this.expandedRows = null;
			},
			formatCurrency(value) {
				return value.toLocaleString('en-US', {style: 'currency', currency: 'USD'});
			},
			formatDate(value) {
				return value.toLocaleDateString('en-US', {
					day: '2-digit',
					month: '2-digit',
					year: 'numeric',
				});
			},
			calculateCustomerTotal(name) {
				let total = 0;
				if (this.customer3) {
					for (let customer of this.customer3) {
						if (customer.representative.name === name) {
							total++;
						}
					}
				}

				return total;
			}
		}
        */
        
	}
</script>

