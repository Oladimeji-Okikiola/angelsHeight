<template>
    <div>
        <!-- Error/Success Messages -->
        <div v-if="store.error" class="error-message">{{ store.error }}</div>
        <h5 v-if="noInput" class="error-message">{{ errorMessage }}</h5>
        
        <!-- Form Section - Shown before submission -->
        <form v-if="!formSubmitted" @submit.prevent="submitRegistration" class="page">
            <p>
                Note: This Page is for Students who has paid the form fee and seeking admission.
            </p>
            
            <div class="stepA">
                <h1>Personal Information</h1>

                <div class="stepA">
                    <h3>Please upload your passport</h3>
                    <label for="passport"><i class="fa fa-file" style="font-size: 40px; cursor: pointer;"></i></label>
                    <input type="file" id="passport" style="display: none;" @change="handlePassportPhoto" accept="image/*" required>
                    <div v-if="passportPreviewUrl" class="preview">
                        <img :src="passportPreviewUrl" alt="Passport Preview" width="100" />
                    </div>
                 </div>
                
                <!-- SURNAME -->
                <label for="surnanme">Surname:</label>
                <input type="text" id="surname" class="contactInput" v-model="store.studentData.surname" required>
    
                <!-- FIRSTNAME -->
                <label for="firstname">Firstname:</label>
                <input type="text" id="firstname" class="contactInput" v-model="store.studentData.firstname" required>
    
                <!-- MIDDLENAME -->
                <label for="middlename">Middlename:</label>
                <input type="text" id="middlename" class="contactInput" v-model="store.studentData.middlename" required>
    
                <!-- DATE OF BIRTH -->
                <label for="dateOfBirth">Date of Birth:</label>
                <input type="date" id="dateOfBirth" class="contactInput" v-model="store.studentData.dateOfBirth" required>
    
                <!-- GENDER -->
                <label for="gender">Gender:</label>
                <select id="gender" class="contactInput" v-model="store.studentData.gender" required>
                    <option>Male</option>
                    <option>Female</option>
                </select>
    
                <!-- RELIGION -->
                <label for="religion">Religion:</label>
                <select id="religion" class="contactInput" v-model="store.studentData.religion" required>
                    <option>Christian</option>
                    <option>Muslim</option>
                    <option>Others</option>
                </select>
    
                <!-- LGV -->
                <label for="lgvt">Local Government:</label>
                <input type="text" id="lgvt" class="contactInput" v-model="store.studentData.localGovernment" required>
    
                <!-- CURRENT HOME ADDRESS -->
                <label for="homeAddress">Current Home Address:</label>
                <input type="text" id="homeAddress" class="contactInput" v-model="store.studentData.homeAddress" required>
    
                <!-- PARENT OR GUARDIAN NAME -->
                <label for="parentG">Parent or Guardian Name:</label>
                <input type="text" id="parentG" class="contactInput" v-model="store.studentData.guardian" required>
    
                <!-- ADDREDD -->
                <label for="pAdd">Permanent Address:</label>
                <input type="text" id="pAdd" class="contactInput" v-model="store.studentData.permanentAddress" required>
    
                <!-- SEC.SCHOOL -->
                <label for="secschool">Secondary School Attended:</label>
                <input type="text" id="secschool" class="contactInput" v-model="store.studentData.secondarySchool" required>
    
                <!-- EXTRA CURRICULA ACTIVITIES -->
                <label for="extracurriculla">Extra Curricula activities:</label>
                <input type="text" id="extracurriculla" class="contactInput" v-model="store.studentData.extraCurricula" required>
    
                <!-- Disabilities -->
                <label for="disa">Physical Disabilities?</label>
                <select id="disa" class="contactInput" v-model="store.studentData.disability" required>
                    <option>No</option>
                    <option>Yes</option>
                </select>
    
                <!-- IF YES -->
                <label for="disab">If Yes, State the Nature:</label>
                <input type="text" id="disab" class="contactInput" v-model="store.studentData.disableContent" :required="store.studentData.disability === 'Yes'" :disabled="store.studentData.disability === 'No'">
    
                <!-- PHONE NUMBER -->
                <label for="phone">Phone Number:</label>
                <input type="text" id="phone" class="contactInput" v-model="store.studentData.phone" required>
    
                <!-- Email -->
                <label for="emaill">Email:</label>
                <input type="email" id="emaill" class="contactInput" v-model="store.studentData.email" required>
    
                <!-- EMERGENCY CONTACTS -->
                 <div class="stepA emergencyy">
                    <h1 class="personTo">Person to be Notified during Emergency</h1>

                    <!-- FULLNAME -->
                    <label for="fullname">Fullname:</label>
                    <input type="text" id="fullname" class="contactInput" v-model="store.studentData.E_fullname" required>

                    <!-- ADDRESS -->
                    <label for="adddre">Address:</label>
                    <input type="text" id="adddre" class="contactInput" v-model="store.studentData.E_address" required>

                    <!-- PHONE NUMBER -->
                    <label for="emergencyPhone">Phone Number:</label>
                    <input type="text" id="emergencyPhone" class="contactInput" v-model="store.studentData.E_phone" required>

                    <!-- EMAIL -->
                    <label for="eee">Email:</label>
                    <input type="text" id="eee" class="contactInput" v-model="store.studentData.E_email" required>
                 </div>
              </div>
            
        
              <div class="stepA">
                <h1>Program to Enroll For</h1>
                
                <!-- FIRST CHOICE -->
                <label for="firstChoice">First Choice:</label>
                <select id="firstChoice" class="contactInput" v-model="store.studentData.firstChoice" required>
                    <option>Environmental Health Technology</option>
                    <option>Community Health Extension Worker (CHEW) Junior</option>
                    <option>Community Health Extension Worker (CHEW) Senior</option>
                    <option>Dental Therapy</option>
                    <option>Pharmacy Technician</option>
                    <option>Opticianry Dispensar</option>
                    <option>Public Health Technology</option>
                    <option>Health Assistant Medical</option>
                    <option>Health Technician</option>
                    <option>Computer Science Technology</option>
                    <option>Nutrition and Dietetics</option>
                    <option>Medical Laboratory Technician</option>
                    <option>Orthopedic Plaster Card</option>
                </select>
    
                <!-- SECOND CHOISE -->
                <label for="secondChoice">Second Choice:</label>
                <select id="secondChoice" class="contactInput" v-model="store.studentData.secondChoice" required>
                    <option>Environmental Health Technology</option>
                    <option>Community Health Extension Worker (CHEW) Junior</option>
                    <option>Community Health Extension Worker (CHEW) Senior</option>
                    <option>Dental Therapy</option>
                    <option>Pharmacy Technician</option>
                    <option>Opticianry Dispensar</option>
                    <option>Public Health Technology</option>
                    <option>Health Assistant Medical</option>
                    <option>Health Technician</option>
                    <option>Computer Science Technology</option>
                    <option>Nutrition and Dietetics</option>
                    <option>Medical Laboratory Technician</option>
                    <option>Orthopedic Plaster Card</option>
                </select>
    
                <!-- EDUCATIONAL BACKGROUND -->
                 <div class="stepA eduBack">
                    <p>List all the schools attended in chronological order</p>
                    <input type="text" class="contactInput" placeholder="School Name" v-model="store.studentData.schoolAttended" required>
                    <select class="contactInput" placeholder="Result Awarded" v-model="store.studentData.resultAwarded" required>
                        <option>WAEC</option>
                        <option>NECO</option>
                        <option>NABTEB</option>
                    </select>
                 </div>

                 <div class="stepA academi">
                    <h3>Please upload your O'level result</h3>
                    <label for="olevel"><i class="fa fa-file" style="font-size: 40px; cursor: pointer;"></i></label>
                    <input type="file" id="olevel" style="display: none;" @change="handleCertificate" accept=".pdf, .jpg, .jpeg, .png" required>
                    <div v-if="certificateFileName" class="file-name">
                        Selected: {{ certificateFileName }}
                    </div>
                 </div>    
               
              </div>
            
            
              <div class="stepA">
                    <h1 class="personTo">Sponsor</h1>

                    <!-- FULLNAME -->
                    <label for="financialName">Fullname:</label>
                    <input type="text" id="financialName" class="contactInput" v-model="store.studentData.S_fullname" required>

                    <!-- ADDRESS -->
                    <label for="financialAddress">Address:</label>
                    <input type="text" id="financialAddress" class="contactInput" v-model="store.studentData.S_address" required>

                    <!-- PHONE NUMBER -->
                    <label for="financialPhone">Phone Number:</label>
                    <input type="text" id="financialPhone" class="contactInput" v-model="store.studentData.S_phone" required>

                    <!--    RELATIONSHIP -->
                    <label for="financialRelat">Relationship:</label>
                    <input type="text" id="financialRelat" class="contactInput" v-model="store.studentData.S_relationship" required>
                 </div>
            
            <div class="stepA buttonSign">
                <h5 v-if="noInput" class="error-message">{{ errorMessage }}</h5>
                <button type="submit" :disabled="store.isLoading">{{ store.isLoading ? 'Registering...' : 'Register' }}</button>
            </div>
        </form>

        <!-- Print/Success Section - Shown after submission -->
        <div v-if="formSubmitted" class="success-container">
            <div class="success-message">
                <h2>Registration Successful!</h2>
                <p>Your form has been successfully submitted and saved to our database.</p>
                <div class="print-actions">
                    <button @click="printForm" class="print-button">Print Registration Form</button>
                    <button @click="goToHome" class="home-button">Return Home</button>
                </div>
            </div>

            <!-- Printable Form Section (hidden until print is clicked) -->
            <div id="printable-form" class="printable-form">
                <div class="print-header">
                    <h1>Student Registration Form</h1>
                    <p>Registration ID: {{ registrationId }}</p>
                    <p>Date: {{ formattedDate }}</p>
                </div>

                <div class="print-section">
                    <h2>Personal Information</h2>
                    <div class="passport-photo">
                        <img :src="store.studentData.passportUrl" alt="Passport Photo" width="150" />
                    </div>
                    <div class="info-grid">
                        <div class="info-row">
                            <div class="info-label">Full Name:</div>
                            <div class="info-value">{{ store.studentData.surname }} {{ store.studentData.firstname }} {{ store.studentData.middlename }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Date of Birth:</div>
                            <div class="info-value">{{ formatDate(store.studentData.dateOfBirth) }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Gender:</div>
                            <div class="info-value">{{ store.studentData.gender }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Religion:</div>
                            <div class="info-value">{{ store.studentData.religion }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Local Government:</div>
                            <div class="info-value">{{ store.studentData.localGovernment }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Current Home Address:</div>
                            <div class="info-value">{{ store.studentData.homeAddress }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Parent/Guardian:</div>
                            <div class="info-value">{{ store.studentData.guardian }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Permanent Address:</div>
                            <div class="info-value">{{ store.studentData.permanentAddress }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Secondary School:</div>
                            <div class="info-value">{{ store.studentData.secondarySchool }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Extra Curricular Activities:</div>
                            <div class="info-value">{{ store.studentData.extraCurricula }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Physical Disabilities:</div>
                            <div class="info-value">{{ store.studentData.disability }}</div>
                        </div>
                        <div v-if="store.studentData.disability === 'Yes'" class="info-row">
                            <div class="info-label">Nature of Disability:</div>
                            <div class="info-value">{{ store.studentData.disableContent }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Phone Number:</div>
                            <div class="info-value">{{ store.studentData.phone }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Email:</div>
                            <div class="info-value">{{ store.studentData.email }}</div>
                        </div>
                    </div>
                </div>

                <div class="print-section">
                    <h2>Emergency Contact</h2>
                    <div class="info-grid">
                        <div class="info-row">
                            <div class="info-label">Full Name:</div>
                            <div class="info-value">{{ store.studentData.E_fullname }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Address:</div>
                            <div class="info-value">{{ store.studentData.E_address }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Phone Number:</div>
                            <div class="info-value">{{ store.studentData.E_phone }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Email:</div>
                            <div class="info-value">{{ store.studentData.E_email }}</div>
                        </div>
                    </div>
                </div>

                <div class="print-section">
                    <h2>Program Information</h2>
                    <div class="info-grid">
                        <div class="info-row">
                            <div class="info-label">First Choice:</div>
                            <div class="info-value">{{ store.studentData.firstChoice }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Second Choice:</div>
                            <div class="info-value">{{ store.studentData.secondChoice }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">School Attended:</div>
                            <div class="info-value">{{ store.studentData.schoolAttended }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Result Awarded:</div>
                            <div class="info-value">{{ store.studentData.resultAwarded }}</div>
                        </div>
                    </div>
                </div>

                <div class="print-section">
                    <h2>Sponsor Information</h2>
                    <div class="info-grid">
                        <div class="info-row">
                            <div class="info-label">Full Name:</div>
                            <div class="info-value">{{ store.studentData.S_fullname }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Address:</div>
                            <div class="info-value">{{ store.studentData.S_address }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Phone Number:</div>
                            <div class="info-value">{{ store.studentData.S_phone }}</div>
                        </div>
                        <div class="info-row">
                            <div class="info-label">Relationship:</div>
                            <div class="info-value">{{ store.studentData.S_relationship }}</div>
                        </div>
                    </div>
                </div>

                <div class="print-footer">
                    <div class="signature-section">
                        <div class="signature-box">
                            <p>_______________________</p>
                            <p>Student's Signature</p>
                        </div>
                        <div class="signature-box">
                            <p>_______________________</p>
                            <p>Official Signature</p>
                        </div>
                    </div>
                    <p class="print-date">Printed on: {{ formattedDate }}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
    import {ref, watch, computed } from 'vue'
    import {useRouter, useRoute} from 'vue-router'
    import {useFormStore} from '@/stores/formcollection'

    const store = useFormStore()
    const router = useRouter()
    const route = useRoute()
    const noInput = ref(false)
    const errorMessage = ref('')

    const paymentId = route.params.id
    const passportPreviewUrl = ref('')
    const certificateFileName = ref('')
    const successMessage = ref('')
    const validationErrors = ref([])
    const showValidationErrors = ref(false)
    const formSubmitted = ref(false)
    const registrationId = ref('')

// Generate a random registration ID
const generateRegistrationId = () => {
    const timestamp = new Date().getTime().toString().slice(-6)
    const random = Math.floor(Math.random() * 10000).toString().padStart(4, '0')
    return `REG-${timestamp}-${random}`
}

// Format date for display
const formatDate = (dateString) => {
    if (!dateString) return ''
    const date = new Date(dateString)
    return date.toLocaleDateString('en-GB', {
        day: '2-digit',
        month: 'short',
        year: 'numeric'
    })
}

// Get today's date formatted
const formattedDate = computed(() => {
    return new Date().toLocaleDateString('en-GB', {
        day: '2-digit',
        month: 'long',
        year: 'numeric'
    })
})

    // Handle passport uploads
    const handlePassportPhoto = (event) => {
        const file = event.target.files[0]
        if (file) {
            store.setPassportPhoto(file)
            passportPreviewUrl.value = URL.createObjectURL(file)
        }
    }
    // UPLOADING THE CERTIFICATE
    const handleCertificate = (event) => {
        const filez = event.target.files[0]
        if (filez) {
            store.setCertificate(filez)
            certificateFileName.value = filez.name
        }
    }

    // WATCHING THE DISABILITY SECTION
    watch(() => store.studentData.disability, (newValue) => {
        if (newValue === "No") {
            store.studentData.disableContent = ""
        }
    })

        // NO TRANSACTION ID FOUND
    watch(() => store.noTransactionId, (newVal) => {
        if (newVal) {
            noInput.value = true
            errorMessage.value = 'Transaction ID not found'
        }
    });
        // ALREADY REGISTERED
    watch(() => store.alreadyRegistered, (newVal) => {
        if (newVal) {
            noInput.value = true
            errorMessage.value = 'You have already Registered'
        }
    });
        // SUCCESSFUL
    watch(() => store.canProceed, (newVal) => {
        if (newVal) {
            successMessage.value = 'Student registration successful!'
            formSubmitted.value = true
            registrationId.value = generateRegistrationId()
            // router.push('/Formsubmitted')
        }
    });

    // Form validation function
const validateForm = () => {
  const errors = []
  
  // Check if passport photo is uploaded
  if (!store.studentData.passportPhoto) {
    errors.push("Please upload your passport photograph")
  }
  
  // Check personal information fields
  if (!store.studentData.surname) errors.push("Surname is required")
  if (!store.studentData.firstname) errors.push("Firstname is required")
  if (!store.studentData.middlename) errors.push("Middlename is required")
  if (!store.studentData.dateOfBirth) errors.push("Date of birth is required")
  if (!store.studentData.gender) errors.push("Gender is required")
  if (!store.studentData.religion) errors.push("Religion is required")
  if (!store.studentData.localGovernment) errors.push("Local government is required")
  if (!store.studentData.homeAddress) errors.push("Current home address is required")
  if (!store.studentData.guardian) errors.push("Parent or guardian name is required")
  if (!store.studentData.permanentAddress) errors.push("Permanent address is required")
  if (!store.studentData.secondarySchool) errors.push("Secondary school attended is required")
  if (!store.studentData.extraCurricula) errors.push("Extra curricula activities is required")
  if (!store.studentData.disability) errors.push("Physical disabilities field is required")
  
  // Check disability content field if disability is "Yes"
  if (store.studentData.disability === "Yes" && !store.studentData.disableContent) {
    errors.push("Please state the nature of your disability")
  }
  
  if (!store.studentData.phone) errors.push("Phone number is required")
  if (!store.studentData.email) errors.push("Email is required")
  
  // Check emergency contact fields
  if (!store.studentData.E_fullname) errors.push("Emergency contact fullname is required")
  if (!store.studentData.E_address) errors.push("Emergency contact address is required")
  if (!store.studentData.E_phone) errors.push("Emergency contact phone number is required")
  if (!store.studentData.E_email) errors.push("Emergency contact email is required")
  
  // Check program fields
  if (!store.studentData.firstChoice) errors.push("First choice program is required")
  if (!store.studentData.secondChoice) errors.push("Second choice program is required")
  
  // Check certificate upload
  if (!store.studentData.certificate) {
    errors.push("Please upload your O'level result")
  }
  
  // Check sponsor fields
  if (!store.studentData.S_fullname) errors.push("Sponsor fullname is required")
  if (!store.studentData.S_address) errors.push("Sponsor address is required")
  if (!store.studentData.S_phone) errors.push("Sponsor phone number is required")
  if (!store.studentData.S_relationship) errors.push("Sponsor relationship is required")
  
  validationErrors.value = errors
  return errors.length === 0
}


    // Submit form
    const submitRegistration = async () => {
        showValidationErrors.value = true
        store.studentData.paymentId = paymentId

        if(!validateForm()){
            window.scrollTo({top:0, behavior: 'smooth'})
            return
        }

        try {
            await store.checkId()

        } catch (error) {
            console.error('Registration failed:', error)
        }
    }
// resend api
// re_itnGjHW7_LvdQrT1G4Cf4b7v9DgY9vxhv

// Print the form
const printForm = () => {
        const printContents = document.getElementById('printable-form').innerHTML
        const originalContents = document.body.innerHTML
        
        // Create a new window with only the form content
        const printWindow = window.open('', '_blank')
        printWindow.document.write(`
            <html>
                <head>
                    <title>Angel's Registration Form</title>
                    <style>
                        body {
                            font-family: Arial, sans-serif;
                            line-height: 1.6;
                            padding: 20px;
                        }
                        .headerWithDet{
                            display: flex;
                            flex-direction: column;
                            justify-content: center;
                            align-items: center;
                            margin-bottom: 10px;
                        }
                        .print-header {
                            text-align: center;
                            margin-bottom: 20px;
                            border-bottom: 2px solid #000;
                            padding-bottom: 10px;
                        }
                        .print-section {
                            margin-bottom: 20px;
                            page-break-inside: avoid;
                        }
                        .print-section h2 {
                            border-bottom: 1px solid #ccc;
                            padding-bottom: 5px;
                        }
                        .info-grid {
                            display: grid;
                            grid-template-columns: 1fr;
                            gap: 8px;
                        }
                        .info-row {
                            display: flex;
                        }
                        .info-label {
                            font-weight: bold;
                            width: 200px;
                        }
                        .info-value {
                            flex: 1;
                        }
                        .passport-photo {
                            text-align: center;
                            margin-bottom: 20px;
                        }
                        .signature-section {
                            display: flex;
                            justify-content: space-between;
                            margin-top: 50px;
                        }
                        .signature-box {
                            text-align: center;
                            width: 200px;
                        }
                        .print-footer {
                            margin-top: 30px;
                            text-align: center;
                            font-size: 12px;
                        }
                        .print-date {
                            margin-top: 30px;
                            text-align: right;
                            font-size: 12px;
                        }
                        .numberes{
                            display: flex;
                            gap: 10px;
                        }
                        @media print {
                            body {
                                margin: 0;
                                padding: 15mm;
                            }
                        }
                    </style>
                </head>
                <body>
                    <div class="headerWithDet">
                        <h1>ANGELS HEIGHT</h1>
                        <p>...Healthcare Training Per Excellence is Our Concern</p>
                        <div class="numberes">
                            <p>09032327228</p>
                            <p>08107812435</p>
                        </div>
                    </div>
                    ${printContents}
                </body>
            </html>
        `)
        
        printWindow.document.close()
        printWindow.focus()
        
        // Print after images have loaded
        setTimeout(() => {
            printWindow.print()
        }, 500)
    }

    // Navigate back to home
    const goToHome = () => {
        router.push('/')
    }





















</script>

<style scoped>
    .validation-errors {
        background-color: #fff3cd;
        color: #856404;
        padding: 15px;
        margin-bottom: 20px;
        border-radius: 4px;
        border-left: 5px solid #ffeeba;
    }
    .preview {
        margin-top: 10px;
        border: 1px solid #ddd;
        padding: 5px;
        display: inline-block;
        border-radius: 4px;
    }

    .validation-errors h3 {
        margin-top: 0;
        font-size: 16px;
    }

    .validation-errors ul {
        margin-bottom: 0;
        padding-left: 20px;
    }
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
.error-message{
    align-items: center;
    text-align: center;
    font-size: 25px;
    color: rgba(248, 45, 45, 0.996);
}
button{
    width: 150px;
    background-color: white;
    color: rgb(84, 8, 112);
    padding: 10px;
    border-radius: 20px;
    cursor: pointer;
}
.stepA{
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    gap: 5px;
    justify-content: center;
    align-items: center;
}
label{
    color: white;
    text-align: center;
    text-align-last: center;
}
.personTo, h3{
    color: white;
    background: none;
}
h1{
    background-color: white;
    color: #6897a7;
    text-align: center;
    padding: 10px;
    margin: 10px 0;
    border-radius: 20px;
}
h5{
    text-align: center;
}

@media (max-width: 768px){
    h1{
        font-size: 19px;
    }
}
</style>