<template>
  <section class="card"
    :class="{
      active: isSelected,
      error: hasError,
      inactive: isUnselected
    }"
  >
    <header class="card__header">
        <span class="card__header__icon">
          <form-icons :name="cardIcon" />
        </span>
      <h2 class="card__header__title">
        {{ cardTitle }}
      </h2>
    </header>
    <div class="card__body">
      <p class="card__body__description">
        {{ cardDescription }}
      </p>
      <p class="card__body__fee">
        <strong class="fee__price">${{ cardPrice }} Application Fee</strong>
        <br />
        <small class="fee__fine-print">non-refundable</small>
      </p>
      <ul class="check-list">
        <li class="check-list__item">
          <h5 class="item__header">Requirements</h5>
        </li>
        <li
          class="check-list__item"
          v-for="requirement in cardRequirements"
          :key="requirement"
        >
          <IconCheck />
          {{ requirement }}
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
  import IconCheck from './IconCheck.vue'
  import FormIcons from './FormIcons'

  export default {
    name: 'Card',
    components: {
      FormIcons,
      IconCheck,
    },
    props: {
      cardDescription: { type: String, required: true },
      cardIcon: { type: String, required: true },
      cardPrice: { type: String, required: true },
      cardRequirements: { type: Array, required: true },
      cardTitle: { type: String, required: true },
      hasError: { type: Boolean, default: false },
      hasSelection: { type: Boolean, default: false },
      isSelected: { type: Boolean, default: false },
    },
    computed: {
      isUnselected() {
        return !!this.hasSelection && !this.isSelected
      },
    },
  }
</script>

<style lang="scss">
  .card {
    background: #fff;
    border: 1px solid #85868c;
    border-radius: 2px;
    display: block;
    margin: 0;
    margin-bottom: 16px;
    padding: 0;
    transition: all .5s;

    .card__header {
      align-items: center;
      background: linear-gradient(-180deg, #fafafa 0%, #ededed 100%);
      border-bottom: 1px solid #85868c;
      color: #004183;
      display: flex;
      flex: 1 1 auto;
      flex-grow: 0;
      justify-content: center;
      padding: 24px;
    }
    .card__header__icon {
      margin-right: 16px;
      flex-shrink: 0;
      padding-top: .1em;
      padding-bottom: .1em;
    }
    .card__header__title {
      color: inherit;
      font: normal 1.25em/1.3 "Circular Medium";
      margin: 0;
    }
    .card__body {
      padding: 24px;
    }
    .card__body__description {
      margin: 0;
      margin-bottom: 1em;
    }
    .card__body__fee {
      margin: 0;
      margin-bottom: 1em;
      padding: 0;
    }
    .fee__price {
      color: #175da7;
      font-family: "Circular Bold";
      font-weight: normal;
      text-transform: uppercase;
    }
    .fee__fine-print {
      color: #6d6d6d;
      font-size: 14px;
    }
    .check-list {
      margin-bottom: 24px;
      padding: 0;
    }
    .check-list__item {
      margin-bottom: 16px;
    }
    .item__header {
      font: normal 1em/1.5 "Circular Medium";
    }

    :not(:hover) &.inactive {
      border-color: #a9abb6;
      color: #6d6d6d;

      .card__header {
        color: #85868c;
        background: #fafafa;
      }

      .card__body {
        color: #6d6d6d;
      }
      .fee__price {
        color: #6d6d6d;
      }
    }

    .picker__option:hover & {
      border-color: #4dbdff !important;
      opacity: 1 !important;

      .card__header {
        background: #fafafa;
      }
    }

    :hover {
      .card__header {
        color: #004183 !important;
      }

      .fee__price {
        color: #175da7 !important;
      }
    }

    &.error {
      border-color: #cd3533;
    }

    &.active {
      border-color: #1178ce;
      box-shadow: 0 0 15px -1px rgba(0,0,0,.5);
      opacity: 1 !important;

      .card__header {
        background: #1178ce !important;
        color: #fff;
      }
    }
  }
</style>
