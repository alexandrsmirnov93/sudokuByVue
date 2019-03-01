<template>
	<div>
		<div v-for="(item, index) in fields" :key = 'index' class = 'string'
			v-bind:class = '{ thirdString: index%3 ==2 }'>
		<input v-for="(item2, index2) in item" class = 'field' :key = 'index2'
			v-bind:class = '{thirdField: index2%3 == 2}'
			v-model = 'fields[index][index2].value'
			/>
		</div>
		<button v-on:click = 'checkIt'>Проверить</button>
	</div>
</template>

<script>
export default {
  data () {
    return {
      fields: [],
    }
  },
  mounted(){
	let x = []
	for(let i =0; i<9; i++){
		let bigArr = []
		for(let j = 0; j<9; j++){
			let smallObj = {id: i + ''+j, value: null}
			bigArr.push(smallObj)
		}
		x.push(bigArr)
	}
	this.fields = x
  },
	methods:{
		checkIt(){
			function error(){
				alert('Ошибка')
			}
			
			for(let i =0; i<this.fields.length; i++){
				for(let j =0; j<this.fields[i].length; j++){
					let value = this.fields[i][j].value
					if( value == null || !Number.isInteger(Number(value)) || Number(value) >9 || Number(value <1)  ){
						error();
						return
					}

					for(let i1=0; i1<this.fields.length; i1++){
						for(let j1 =0; j1<this.fields[i1].length; j1++){
							let value1 = this.fields[i1][j1].value
							if((i==i1 && j !=j1) || (j==j1 && i !=i1)){
								if(value == value1){
									error()
									return
								}
							}
							if(Math.floor(i/3) == Math.floor(i1/3) && Math.floor(j/3) == Math.floor(j1/3) && i!=i1 && j !=j1 ){
								if(value == value1){
									error()
									return
								}
							}
						}
					}
			
				}
			}		
			alert('Все ОК')
			return
		}
	}
}
</script>

<style>
.field{
  width: 20px;
}

.thirdString{
	margin-bottom: 10px;
}

.thirdField{
  margin-right: 10px;
}
</style>
