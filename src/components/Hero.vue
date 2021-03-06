<template>
  <div class="hero-wrapper">
    <a :href="linkURL" class="wrapper-link">
      <article class="hero" :style="backgroundImageStyle">
        <div class="textual-content">
          <slot></slot>
        </div>
      </article>
    </a>
  </div>
</template>

<script>
export default {
  name: 'Hero',

  props: ['linkURL', 'backgroundImageURL'],

  computed: {
    // Returns properly formatted style object
    backgroundImageStyle: function() {
      if (typeof this.backgroundImageURL === 'string' && this.backgroundImageURL.length > 0) {
        return {'background-image': 'url("' + this.backgroundImageURL +'")'};
      } else {
        return {};
      }
    }
  }
}
</script>

<style lang="scss" scoped>

@import '../assets/scss/vars';

.wrapper-link {
  display: block;
  color: #fff;
  font-size: 1rem;
  margin: 0 auto;
  max-width: calc(#{$max-width} + #{$default-gutter * 3});
}

.hero {
  position: relative;
  background-size: cover;

  &:before {
    // Locks the aspect ration of the card image
    content: '';
    position: relative;
    display: block;
    box-sizing: content-box;
    padding: 0 0 #{1 * 100%};
    @include breakpoint-min(phablet) {
      padding: 0 0 #{2 / 3 * 100%};
    }
    @include breakpoint-min(tablet) {
      padding: 0 0 #{2 / 3.75 * 100%};
    }
    @include breakpoint-min(full) {
      padding: 0 0 #{2 / 5 * 100%};
    }
  }

  &:after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    z-index: 0;
    display: block;
    width: 100%;
    height: 100%;
    background:
      linear-gradient(180deg,rgba(0,0,0,0.6) 0%,
      rgba(0,0,0,0.35) 36.04%,
      rgba(0,0,0,0.55) 100%);
  }

  // Need these because of default colors set for tags :(
  h1,
  h2,
  h3,
  h4,
  h5,
  h6,
  p {
    color: #fff;
  }

  // Need these because of default colors set for tags :(
  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    font-size: $base-line-height;
    line-height: 1.3;
    font-weight: bold;
    @include breakpoint-min(phone) {
      font-size: $base-line-height * 1.25;
    }
    @include breakpoint-min(phablet) {
      font-size: $base-line-height * 1.75;
    }
    @include breakpoint-min(tablet) {
      font-size: $base-line-height * 2;
    }
    @include breakpoint-min(laptop) {
      font-size: $base-line-height * 2.6725;
    }
  }

}

.textual-content {
  position: absolute;
  top: 50%;
  left: 0;
  z-index: 1;
  width: 100%;
  transform: translate(0, -50%);
  padding: 0 $default-gutter;
  @include breakpoint-min(laptop){
    padding: 0 #{$default-gutter * 2};
  }
  @include breakpoint-min(full) {
    left: 50%;
    transform: translate(-50%, -50%);
    padding: 0 #{$default-gutter * 2.5};
  }
}

.content-type {
  color: #F7D7A7;
  font-size: 0.875em;
  font-weight: 600;
}

p {
  font-style: italic;
  @include breakpoint-min(tablet) {
    font-size: 1.125em;
  }
}

</style>
