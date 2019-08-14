<template>
    <div id="employee-form">
        <form @submit.prevent="handleSubmit">
            <label>Employee Name</label>
            <input 
                ref="first"
                type="text"
                :class="{ 'has-error': submitting && isNameValid }"
                v-model="employee.name"
                @focus="clearStatus"
                @keypress="clearStatus" 
            />
            <label>Employee Email</label>
            <input 
                type="text"
                :class="{ 'has-error': submitting && isEmailValid }"
                v-model="employee.email"
                @focus="clearStatus"
            />
            <p v-if="error && submitting" class="error-message">
                ❗Please fill out all required fields and valid email address
            </p>
            <p v-if="success" class="success-message">
                ✅ Employee successfully added
            </p>
            <button>Add Employee</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'employee-form',
    data() {
        return{
            submitting: false,
            error: false,
            success: false,
            employee: {
                name: '',
                email: '',
                reg: /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,24}))$/,
            },
        }
    },
    methods: {
        handleSubmit() {
            this.submitting = true
            this.clearStatus()

            if(this.isNameValid || this.isEmailValid){
                this.error = true
                return
            }

            this.$emit('add:employee', this.employee)
            this.$refs.first.focus()
            this.employee = {
                name: '',
                email: '',
                reg: /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,24}))$/,
            }
            this.error = false
            this.success = true
            this.submitting = false
        },

        clearStatus() {
            this.success = false
            this.error = false
        },
    },
    computed: {
        isNameValid() {
            return this.employee.name === '';
        },
        isEmailValid () {
            return (this.employee.email === '') ? true : (this.employee.reg.test(this.employee.email)) ? false : true;
        }
    },
}
</script>

<style scoped>
    form {
        margin-bottom: 2rem;
    }

    [class*='-message'] {
        font-weight: 500;
    }

    .error-message {
        color:#d33c40;
    }

    .success-message {
        color: #32a95d;
    }
</style>