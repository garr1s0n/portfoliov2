<template>
    <div class="container">
      <div>
        <div class="row">
            <div class="headerText column twelve">
                <h1 class="title">send me a message!</h1>
                <p>Interested in doing business? Want to learn more? Just want to say hi? Fill out the form below and drop me a line!</p>
                <transition name="fade">
                    <p v-if="contactSent" class="postSubmit">Thanks for the message! I'll get back to you soon.</p>
                </transition>
            </div>
        </div>
        <form id="contact-form" method="post" action="https://sheltered-coast-37245.herokuapp.com/send" @submit.prevent="contactSubmit()" >
            <div class="row">
                <div class="six columns">
                    <label for="exampleEmailInput">Full Name:</label>
                    <input class="u-full-width" type="text" placeholder="Name..." id="name" name="name" v-model="name" >
                </div>
                <div class="six columns">
                    <label for="exampleEmailInput">Company Name:</label>
                    <input class="u-full-width" type="text" placeholder="Company..." id="company" name="company" v-model="company" >
                </div>
            </div>
            <div class="row">
                <div class="six columns">
                    <label for="exampleEmailInput">Email Address:</label>
                    <input class="u-full-width" type="email" placeholder="Email Address..." id="email" name="email" v-model="email" >
                </div>
                <div class="six columns">
                    <label for="exampleEmailInput">Phone Number:</label>
                    <input class="u-full-width" type="tel" placeholder="Phone Number..." id="phone" name="phone" v-model="phone" >
                </div>
            </div>
            <div class="row">
            <div class="twelve columns">
                    <label for="exampleMessage">Message</label>
                    <textarea class="u-full-width" placeholder="Hello!" id="message" name="message" v-model="message" ></textarea>
                </div>
            </div>
            <div class="row">
                <div class="twelve columns">
                    <button class="button--white" type="submit" value="Submit">Submit</button>
                </div>
            </div>
        </form>
      </div>
    </div>
</template>

<script>
import Vue from 'vue'
import VeeValidate from 'vee-validate'

export default {
  data: function () {
    return {
      name: "",
      company: "",
      email: "",
      phone: "",
      message: "",
      contactSent: false
    }
  },
  mounted: function () {
    Vue.use(VeeValidate)
  },
  methods: {
    contactSubmit: function () {
    //   this.contactFormData.append("name",this.name);
    //   this.contactFormData.append("company",this.company);
    //   this.contactFormData.append("email",this.email);
    //   this.contactFormData.append("phone",this.phone);
    //   this.contactFormData.append("message",this.message);

    //   var request = new XMLHttpRequest();

    //   console.log(this.contactFormData); 
    
      document.getElementById('contact-form').submit()

      document.getElementById('contact-form').reset()
      this.contactSent = !this.contactSent
      setTimeout(function () {
        this.contactSent = !this.contactSent
      }, 600)
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

