<template>
    <div>
        <div v-show="isNotDirty">
            <clipboard
                @success="handleSuccess"
                @error="handleError"
                :value="value" />
        </div>

        <div v-show="success">
            <success-icon />
        </div>

        <div v-show="error">
            <error-icon />
        </div>
    </div>
</template>

<script>
import Clipboard from './Clipboard'
import SuccessIcon from './Icons/Success'
import ErrorIcon from './Icons/Error'

export default {
    props: ['value'],
    components: {
        Clipboard,
        SuccessIcon,
        ErrorIcon
    },
    data () {
        return {
            success: false,
            error: false,
        }
    },
    methods: {
        handleSuccess () {
            this.reset()
            this.success = true
        },
        handleError () {
            this.reset()
            this.error = true
        },
        reset () {
            setTimeout(() => {
                this.success = false
                this.error = false
            }, 2300)
        }
    },
    computed: {
        isNotDirty () {
            return ! this.success && ! this.error
        }
    }
}
</script>
