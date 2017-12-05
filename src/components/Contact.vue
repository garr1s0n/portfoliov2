<template>
    <div class="container">
      <div class="contactSection">
        <div class="row">
            <div class="headerText column twelve">
                <h1 class="title">send me a message!</h1>
                <p>Interested in doing business? Want to learn more? Just want to say hi? Fill out the form below and drop me a line!</p>
            </div>
        </div>
        <form id="siteContactForm" @submit.prevent>
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
            
            document.getElementById('siteContactForm').reset()

            console.log('Form Submitted')
        }
    }
}
</script>

<<style lang="less">
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

.contactSection .title {
  font-family: @playfair;
  display: block;
  font-weight: 900;
  font-size: 5vw;
  line-height: 1;
  color: #fff;
}

.contactSection .title + p {
    font-size: .875em;
    margin: 0 0 1em;
}

fieldset { 
    margin: 0 -.5rem; 
}

.vue-form-generator {
    .form-group {
        width: ~"calc(50% - 1rem)";
        margin: 0 .5rem 1rem;
    }
    
    .form-group.error .errors {
        color: red;
        font-size: .8rem;
        line-height: 1.4;
        position: relative;
        top: -.25em;
    }
    .form-group.error.field-textArea .errors {
        top: -1em;
    }

    .form-group.field-textArea, .form-group.field-submit {
        width: ~"calc(100% - 1rem)";
    }
    .form-group.field-submit {
        margin-bottom: 0; 
    }

    @media screen and (max-width: 48em) {
        .form-group, .form-group.field-textArea {
            width: 100%;
            margin: 0 0 1rem;
        }
    }

    input.form-control, textarea.form-control {
        border: 1px solid #fff;
        background: none;
        color: #fff;
        font-size: .725em;
        margin: 0 0 .25rem;
        resize: none;
        transition: all .35s ease-in-out;
    }

    textarea.form-control { 
        height: 10em;
    }

    .hint {
        font-size: .725rem;
        line-height: 1;
        text-align: right;
        color: #fff;
    }

    .field-wrap { 
        input[type=submit] {
            display: inline-block;
            font-size: 1em;
            border-radius: .25em;
            text-decoration: none;
            height: auto;
            padding: .5em 2em;
            margin: 0;
            transition: all .35s ease-in;
            border: 1px solid #fff !important;
            color: #fff !important;
            background: none !important;
            
        }
        input[type=submit]:hover {
            color: @blue !important;
            background: #fff !important;
        }
        @media screen and (max-width: 30em) {
            input[type=submit] {
                font-size: .825em;
                padding: .25em 1em;
            }
        }
    }

}

@media screen and (max-width: 48em) {
    fieldset {
        margin: 0;
    }
}

.vue-form-generator .form-group label {
    font-size: .5em; 
    font-weight: 700;
    margin-bottom: .15em;
    color: #fff;
    letter-spacing: 0.02em;
}

.vue-form-generator 
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
.vue-form-generator input.form-control:focus, .vue-form-generator textarea.form-control:focus {
    border: 1px solid #000;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to {
  opacity: 0
}

</style>

