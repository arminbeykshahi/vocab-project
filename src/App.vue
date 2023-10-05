<template>
 
 <div class="main mt-5">
    <div class="container">
        <div class="row g-4">
            <div class="col-md-6">

                <div v-if="namayeshalert" class="alert alert-danger">

                    لطفا تمامی فیلد ها را پر کنید

                </div>

                <form @submit.prevent="validation">
                  
                 <div class="mb-4">
                 <label for="loghat" class="form-label">لغت : </label>
                 <input type="text" v-model="loghatmeghdar" class="form-control" id="loghat">
                 </div>

                <div class="mb-4">
                <label for="mani" class="form-label">معنی : </label>
                <input type="text" v-model="manimeghdar" class="form-control" id="mani">
                </div>

                <button type="submit" class="btn btn-success w-100">افزودن لغت</button>

                </form>
            </div>
            <div class="col-md-6">
                <ul class="mt-4">
                    <li v-for=" word in words" :key="word.id" class="d-flex justify-content-between mb-3">
                        <div class="detail d-flex">
                            <div class="me-2 ms-2">{{word.nameloghat}}</div>
                                 :
                            <div class="ms-2">{{word.manieloghat}}</div>
                        </div> 

                           <i @click="deleteitem(word.nameloghat)" class="bi bi-x-lg ms-auto text-danger"></i>
                    </li>
                </ul>
                 <span v-if="namayeshtedad" class="mt-5 ms-5">
                        تعداد لغت : 
                        <span>{{words.length}}</span>
                 </span>
                 
                 
            </div>
        </div>
    </div>
 </div>

</template>

<script>
import { reactive, ref } from 'vue'
import Swal from 'sweetalert2'


export default {
    
    setup () {

        const loghatmeghdar = ref('')
        const manimeghdar = ref('')
        const namayeshalert = ref(true)
        const words = ref([])
        const namayeshtedad = ref(false)


        function validation() {
            
             if (loghatmeghdar.value !== '' && manimeghdar.value !== '') {
                
                namayeshalert.value = false

                const word = reactive({

                nameloghat: loghatmeghdar.value,
                manieloghat: manimeghdar.value

                })

                words.value.push(word)

                console.log(words.value);
                
                Swal.fire(
                'موفق',
                'لغت اضافه شد',
                'success'
                )

                namayeshtedad.value = true

  
             }

             else {

                namayeshalert.value = true
             }
        }

        validation()


        function deleteitem(name) {

          words.value =  words.value.filter(word=>word.nameloghat !== name)
            
        }



        return {loghatmeghdar,manimeghdar,namayeshalert,validation,words,namayeshtedad,deleteitem}
    }
}

  
</script>

<style>

html {

    direction: rtl;
}

.detail {

    width: 75%;
    height: 100%;
}


ul li {

    border: 1px solid gray;
    border-radius: 10px;
    padding: 5px;
}


.bi-x-lg {

    cursor: pointer;
}

</style>
