<template>
    <div class="container">
      <div>
        <div class="row">
            <div class="headerText column twelve">
                <h1 class="title">send me a message!</h1>
                <p>Interested in doing business? Want to learn more? Just want to say hi? Fill out the form below and drop me a line!</p>
            </div>
        </div>
        <form id="siteContactForm">
            <vue-form-generator :schema="schema" :model="model" :options="options">
            </vue-form-generator>
        </form>
      </div>
    </div>
</template>

<script>
import Vue from 'vue'
import VueFormGenerator from "vue-form-generator"
    import "vue-form-generator/dist/vfg-core.css"
import Cleave from "cleave.js"
    require('cleave.js/dist/addons/cleave-phone.US')
import Axios from "axios"

Vue.use(VueFormGenerator)

export default {
    components: {
        "vue-form-generator": VueFormGenerator.component
    },
    data: function () {
        return {
            model: {
                fullName: "",
                companyName: "",
                emailAddress: "",
                phoneNumber: "",
                message: ""
            },
            schema: {
                fields: [
                    {
                        id: "fullName",
                        type: "input",
                        inputType: "text",
                        label: "Full Name: ",
                        model: "fullName",
                        maxlength: 50,
                        required: true,
                        validator: VueFormGenerator.validators.string
                    },
                    {
                        id: "companyName",
                        type: "input",
                        inputType: "text",
                        label: "Company Name: ",
                        model: "companyName",
                        maxlength: 65,
                        required: false
                    },
                    {
                        id: "emailAddress",
                        type: "input",
                        inputType: "email",
                        label: "Email Address: ",
                        model: "emailAddress",
                        maxlength: 50,
                        required: true,
                        placeholder: "Your Email Address",
                        validator: VueFormGenerator.validators.email
                    },
                    {
                        id: "phoneNumber",
                        type: "cleave",
                        label: "Phone Number: ",
                        model: "phoneNumber",
                        required: true,
                        cleaveOptions: {
                            blocks: [0, 3, 0, 3, 4],
                            delimiter: ' ',
                            delimiters: ['(', ')', ' ', '-', '-'],    
                            numericOnly: true,
                            uppercase: false,
                            lowercase: false
                        },
                        validator: VueFormGenerator.validators.string
                    },
                    {
                        id: "message",
                        type: "textArea",
                        label: "Message: ",
                        model: "message",
                        max: 1000,
                        placeholder: "What can I do for you?",
                        rows: 3,
                        hint: "Max 1,000 characters",
                        required: true,
                        validator: VueFormGenerator.validators.string
                    },
                    {
                        id: "submitBtn",
                        type: "submit",
                        buttonText: "Submit",
                        validateBeforeSubmit: true,
                        onSubmit: this.formSubmit
                    }
                ]
            },
            options: {
                validateAfterChanged: true
            }
        }
    },
    methods: {
        formSubmit: function () {
            console.log('Form Processing')

            //name company email phone message
            const contactName = this.model.fullName
            const contactCompany = this.model.companyName
            const contactEmail = this.model.emailAddress
            const contactPhone = this.model.phoneNumber
            const contactMessage = this.model.message
            
            Axios.post('https://sheltered-coast-37245.herokuapp.com/send', {
                name: contactName,
                company: contactCompany,
                phone: contactPhone,
                email: contactEmail,
                message: contactMessage
            })
            .then(function (response) {
                console.log(response);
            })
            .catch(function (error) {
                console.log(error);
            });
            
            console.log('Form Submitted')
        }
    }
}
</script>

<<style lang="less" scoped>
@import url('../assets/styles/base-styles.less');

.formSubmitSrc { 
    width: 1px;
    height: 1px;
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
    overflow: hidden;
    opacity: 0;
    visibility: hidden;
}

.title {
  font-family: @playfair;
  display: block;
  font-weight: 900;
  font-size: 5vw;
  line-height: 1;
  color: #fff;
}

.title + p {
    font-size: .875em;
    margin: 0 0 1em;
}

label {
    font-size: .5em; 
    font-weight: 700;
    margin-bottom: .15em;
    color: #fff;
    letter-spacing: 0.02em;
}

input, textarea {
    border: 1px solid #fff;
    background: none;
    color: #fff;
    font-size: .725em;
    transition: all .35s ease-in-out;
}
::-webkit-input-placeholder { 
  color: rgba(255,255,255,0.75);
}
::-moz-placeholder {
  color: rgba(255,255,255,0.75);
}
:-ms-input-placeholder {
  color: rgba(255,255,255,0.75);
}
:-moz-placeholder { 
  color: rgba(255,255,255,0.75);
}
input:focus, textarea:focus {
    border: 1px solid #000;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to {
  opacity: 0
}

</style>

