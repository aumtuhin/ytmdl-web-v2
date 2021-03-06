<template>
  <div class="static__container">
    <div
      class="content md:w-2/5 md:px-0 px-4 mr-auto ml-auto"
      v-html="getContent"
    ></div>
  </div>
</template>

<script>
import snarkdown from "snarkdown";

export default {
  name: "StaticContent",
  props: {
    filePath: {
      type: String
    }
  },
  data: () => {
    return {
      content: ""
    };
  },
  methods: {
    readContent: function() {
      /**
       * Read the content of the passed file based on
       * the path and accordingly store it in a local
       * variable.
       */
      fetch(this.getFilePath)
        .then(response => {
          return response.text();
        })
        .then(text => {
          this.content = snarkdown(text);
        });
    }
  },
  computed: {
    getContent() {
      return this.content;
    },
    getFilePath() {
      return this.filePath;
    }
  },
  mounted() {
    this.readContent();
  }
};
</script>

<style lang="scss" scoped>
.static__container {
  @apply my-5;

  @extend .roboto;
  font-size: 18px;

  @apply text-gray-600;

  .content {
    ::v-deep h1,
    ::v-deep h2,
    ::v-deep h3,
    ::v-deep h4 {
      @extend .work-sans;

      color: $black;
      margin: 2rem 0;
      font-weight: 500;

      @media only screen and (max-width: $md) {
        margin: 1.5rem 0;
      }
    }

    ::v-deep h1 {
      font-size: 2.2em;
      font-weight: 700;
    }

    ::v-deep h2 {
      font-size: 1.8em;
      font-weight: 600;
    }

    ::v-deep h3 {
      @apply text-gray-700;

      font-size: 1.6em;
      font-weight: 600;
    }

    ::v-deep h4 {
      font-size: 1.3em;
      font-weight: 400;
    }

    ::v-deep p,
    ::v-deep li {
      @extend .roboto;
      font-size: 18px;

      @apply text-gray-600;
    }

    ::v-deep ul {
      display: block;
      list-style-type: disc;
      margin-block-start: 1em;
      margin-block-end: 1em;
      margin-inline-start: 0px;
      margin-inline-end: 0px;
      padding-inline-start: 20px;
    }

    ::v-deep code {
      background: $yellow;
      color: $orange;
    }

    ::v-deep a {
      color: $darkgreen;
      text-decoration: underline;
    }

    ::v-deep blockquote {
      @apply my-4;
      @apply py-2;
      @apply pl-2;
      @apply pr-1;
      @apply rounded-sm;

      background: $yellow;
      border-left: 10px solid darken($yellow, 10);
    }

    @media only screen and (max-width: $md) {
      ::v-deep h1 {
        font-size: 2em;
      }

      ::v-deep h2 {
        font-size: 1.8em;
      }

      ::v-deep h3 {
        font-size: 1.6em;
      }

      ::v-deep h4 {
        font-size: 1.2em;
      }
    }
  }
}
</style>
