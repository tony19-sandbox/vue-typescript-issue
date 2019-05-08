> Demo for https://stackoverflow.com/q/56002310/6277151

Demonstrates a workaround for TypeScript errors in the following code, caused by the omitted return type for `profilePath` (which uses `this.$store` to compute its return value):

```
<script lang='ts'>
import Vue from 'vue';

export default Vue.extend({
  data: function() {
    return {
      open: false
    }
  },
  computed: {
    profilePath: function() {
      return "/user/" + this.$store.state.profile.profile.user.id
    }
  },
  methods: {
    toggle: function () {
      this.open❌ = !this.open❌
      if (this.open❌) {
        // Add click listener to whole page to close dropdown
        document.addEventListener('click', this.close❌)
      }
    },
    close: function () {
      this.open❌ = false
      document.removeEventListener('click', this.close❌)
    }
  }
})
</script>
```

The workaround is to [specify `string` as the return type for `profilePath`](https://github.com/tony19-sandbox/vue-typescript-issue/blob/423172b/src/components/Foo.vue#L17).

### Steps to reproduce

 1. Clone this repo with `git clone https://github.com/tony19-sandbox/vue-typescript-issue.git` and CD into the directory.

 2. Run `npm run build` to build the project.

 3. Observe no errors.

 4. On [`src/components/Foo.vue#L17`](https://github.com/tony19-sandbox/vue-typescript-issue/blob/423172b/src/components/Foo.vue#L17), remove the return type from `profilePath`.

 5. Run `npm run build` to build the project.

 6. Observe the following build error on every reference to `this.open` and `this.close`:

 > `Property 'XXX' does not exist on type 'CombinedVueInstance<Vue, {}, {}, {}, Readonly<Record<never, any>>>'`