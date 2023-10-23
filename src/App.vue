<template>
	<div class="form">
		<form>
			<div class="row">
				<label for="city-select">Город</label>
				<select name="city" v-model="selectedCity">
					<option value=""></option>
					<option v-for="(city, cityId) in database" :value="cityId">{{ city.name }}</option>
				</select>
			</div>
			<div class="row">
				<label for="dep-select">Цех</label>
				<select name="department" v-model="selectedDepartment">
					<option value=""></option>
					<option v-for="(department, departmentId) in selectedCityDepartments" :value="departmentId">{{ department.name }}</option>
				</select>
			</div>
			<div class="row">
				<label for="staff-select">Сотрудник</label>
				<select name="staff" v-model="selectedStaff">
					<option value=""></option>
					<option v-for="employee in selectedDepartmentEmployees" :value="employee">{{ employee }}</option>
				</select>
			</div>
			<div class="row">
				<label for="team-select">Бригада</label>
				<select name="team" v-model="selectedTeam">
					<option value=""></option>
					<option value="1st">Первая</option>
					<option value="2nd">Вторая</option>
				</select>
			</div>
			<div class="row">
				<label for="shift-select">Смена</label>
				<select name="shift" v-model="selectedShift">
					<option value=""></option>
					<option value="1st">Первая</option>
					<option value="2nd">Вторая</option>
				</select>
			</div>
			<div class="row">
				<input type="submit" value="Отправить" class="send">
			</div>
		</form>
	</div>
</template>

<script>
export default {
	data() {
		return {
		database: {
			sev: {
				name: "Севастополь",
					departments: {
						rel: {
							name: "Выпускающий",
							employees: ["Иванов", "Смирнов", "Кузнецов"]
						}
				}
			},
			sim: {
				name: "Симферополь",
				departments: {
					rel: {
						name: "Выпускающий",
						employees: ["Попов", "Васильев", "Петров"]
					}
				}
			},
			yal: {
			name: "Ялта",
				departments: {
					pre: {
						name: "Заготовительный",
						employees: ["Соколов", "Михайлов", "Новиков"]
					},
					rel: {
						name: "Выпускающий",
						employees: ["Федоров", "Морозов", "Волков"]
					},
				}
			},
			alu: {
				name: "Алушта",
				departments: {
					pre: {
						name: "Заготовительный",
						employees: ["Алексеев", "Лебедев", "Семенов"]
					},
					rel: {
						name: "Выпускающий",
						employees: ["Егоров", "Павлов", "Козлов"]
					}
				},
			},
			dja: {
				name: "Джанкой",
				departments: {
					pre: {
						name: "Заготовительный",
						employees: ["Степанов", "Николаев", "Орлов"]
					},
					pro: {
						name: "Обрабатывающий",
						employees: ["Андреев", "Макаров", "Никитин"]
					}
				}
			},
			evp: {
				name: "Евпатория",
				departments: {
					pre: {
						name: "Заготовительный",
						employees: ["Захаров", "Зайцев", "Соловьев"]
					},
					pro: {
						name: "Обрабатывающий",
						employees: ["Борисов", "Яковлев", "Григорьев"]
					}
				}
			},
		},
		selectedCity: '',
		selectedDepartment: '',
		selectedStaff: '',
		selectedTeam: '',
		selectedShift: ''
		};
	},
	computed: {
		selectedCityDepartments() {
			if (this.selectedCity) {
				return this.database[this.selectedCity].departments;
			}
			return {};
		},
		selectedDepartmentEmployees() {
			if (this.selectedCity && this.selectedDepartment) {
				return this.database[this.selectedCity].departments[this.selectedDepartment].employees;
			}
			return [];
		}
	},
	watch: {
		selectedCity: 'clearSelection',
		selectedDepartment: 'clearSelection'
	},
	methods: {
		clearSelection() {
			this.selectedStaff = '';
		}
	}
};
</script>

<style scoped>
* {
	border: none;
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}

body {
	background: rgb(214, 49, 49);
}

.form {
	margin: 40px auto;
	padding: 40px;
	background: rgb(227, 221, 221);
	display: block;
	height: 75vh;
	width: 500px;
	border-radius: 15px;
	box-shadow: 0 0 20px;
}

.row {
	display: flex;
	background: rgb(173, 173, 176);
	padding: 15px;
	border-radius: 5px;
	margin-bottom: 20px;
	justify-content: space-between;
}

label {
	font-size: 20px;
}

select {
	font-size: 15px;
	text-align: center;
	border-radius: 10px;
	width: 175px;
	border: 1px solid black; 
	padding: 5px; 
}

.send {
	background: white;
	padding: 10px 20px;
	border: none;
	border-radius: 5px;
	cursor: pointer;
	font-size: 16px;
	transition: background 0.3s;
	margin: 0 auto;
}

.send:hover {
	background: rgb(214, 49, 49);
}


</style>
