<template>
    <div>
        <!-- REGISTRATION FOR ADMIN -->
        <div class="page">
            <h5 v-if="registerE">{{ registerError }}</h5>
            <input type="text" class="contactInput" placeholder="Please input your Fullname" v-model="lecturerDetails.fullname">
            <p v-if="nameError" class="errorClass">{{ nameError }}</p>
            <input type="text" class="contactInput" placeholder="Please input your Phone Number" v-model="lecturerDetails.phone">
            <input type="email" class="contactInput" placeholder="Please input your email" v-model="lecturerDetails.email">
            <p v-if="emailError" class="errorClass">{{ emailError }}</p>
            <input :type="passwordVisible ? 'text' : 'password'" class="contactInput" placeholder="Password" v-model="lecturerDetails.password">
            <p v-if="passwordError" class="errorClass">{{ passwordError }}</p>
            <div class="buttons">
                <button @click.prevent="togglePasswordVisibility" type="button">{{ passwordVisible ? 'Hide' : 'Show' }} Password </button>
                <button @click="registerLecturer" :disabled="auth.isLoading">{{ auth.isLoading ? 'Registering...' : "Register"}}</button>
            </div>
        </div>
    </div>
</template>

<script setup>
    import {ref, watch} from 'vue'
    import {useRouter} from 'vue-router'

    const router = useRouter()
    import {useAuthStore} from '@/stores/registration'
    const auth = useAuthStore()
    const nameError = ref('')
    const passwordError = ref('')
    const emailError = ref('')


    // REGISTRATION ERROR
    const registerError = ref('')
    const registerE = ref(false)

    // AUTHENTICATING THE INPUT
    const namePattern = /^[A-Za-z]+(?:\s[A-Za-z]+){1,2}$/
    const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
    const passwordPattern = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[\W_]).{8,40}$/

    // REGISTRATION DETAILS
    const lecturerDetails = ref({
        fullname : '',
        phone: '',
        email: '',
        password: ''
    })
    // REGISTRATION FUNCTION
    const registerLecturer = async () => {
        // CHECK NAME
        if(!namePattern.test(lecturerDetails.value.fullname)){
            nameError.value = 'Name must contain two to three words'
            return
        }
        nameError.value = ''
        // CHECK EMAIL
        if(!emailPattern.test(lecturerDetails.value.email)){
            emailError.value = 'Invalid Email Format'
            return
        }
        emailError.value = ''
        // CHECK PASSWORD
        if(!passwordPattern.test(lecturerDetails.value.password)){
            passwordError.value = 'Password must be at least 8 characters long \nmust include an UPPER CASE \na lower case \na special character'
            return
        }
        passwordError.value = ''

    
        // CHECK FOR EMPTY SPACES
        if(lecturerDetails.value.email == '' || lecturerDetails.value.password == '' || lecturerDetails.value.fullname == '' || lecturerDetails.value.phone == ''){
            registerE.value = true
            registerError.value = 'Please Fill all Fields'
            return
        }
        
        await auth.registerLecturer(lecturerDetails.value)
    }

    // WATCH FOR AUTHENTICATION TO PROCEED TO THE PAGE FOR EMAIL CONFIRMATION
    watch(() => auth.canLecture, (newVal) => {
        if (newVal) {
            router.push('/confirm-email')
        }
    });



    const passwordVisible = ref(false)
    const togglePasswordVisibility = () => {
        passwordVisible.value = !passwordVisible.value
    }
</script>

<style scoped>
    .page{
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        gap: 10px;
        background-color: #6897a7;
        margin: 10px;
        padding: 20px;
        border-radius: 10px;
        box-shadow: inset 10px 6px 50px rgb(26, 49, 195);
    }
    .errorClass{
        color: red;
    }
.page p{
    text-align: center;
    color: white;
    font-size: 25;
}
.contactInput{
    width: 300px;
    border-radius: 10px;
    height: 35px;
    border: none;
    outline: none;
    padding: 10px;
    box-shadow: inset 10px 6px 50px rgb(192, 192, 196);
}
.buttons{
    display: flex;
}
h5{
    font-size: 20px;
    color: rgba(179, 20, 20, 0.996);
}
button{
    width: 150px;
    background-color: white;
    color: rgb(84, 8, 112);
    padding: 10px;
    border-radius: 20px;
    cursor: pointer;
}
span{
    color: white;
    cursor: pointer;
}
h3{
    margin: 5px auto;
    text-align: center;
    text-align-last: center;
}
@media (max-width: 768px){
    span{
    color: white;
    cursor: pointer;
}
h3{
    margin: 5px auto;
    text-align: center;
    text-align-last: center;
    display: flex;
    flex-direction: column;
}
}
</style>