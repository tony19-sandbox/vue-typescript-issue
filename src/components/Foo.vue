<template>
  <div class="foo">
    MyFoo {{profilePath}}
  </div>
</template>

<script lang='ts'>
    import Vue from 'vue';

    export default Vue.extend({
        data: function() {
            return {
                open: false
            }
        },
        computed: {
            profilePath: function(): string {
                return "/user/" + this.$store.state.profile.profile.user.id
            }
        },
        methods: {
            toggle: function () {
                this.open = !this.open

                if (this.open) {
                    // Add click listener to whole page to close dropdown
                    document.addEventListener('click', this.close)
                }
            },
            close: function () {
                this.open = false;
                document.removeEventListener('click', this.close)
            }
        }
    })
</script>