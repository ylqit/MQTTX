<template>
  <div class="empty-page right-content">
    <div class="empty-page__block">
      <div>
        <img :src="imageSrc" alt="new connection" />
      </div>
      <el-button class="primary-btn" icon="el-icon-plus" @click="clickMethod(false)">
        {{ btnTitle }}
      </el-button>
      <i18n path="common.cloud" tag="p">
        <template #cloud>
          <a :href="emqxCloudWebsite" target="_blank" rel="noopener noreferrer">EMQX Cloud</a>
        </template>
      </i18n>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator'
import { Getter } from 'vuex-class'
import gaCustomLinks from '@/utils/gaCustomLinks'

@Component
export default class EmptyPage extends Vue {
  @Prop({ required: true }) public btnTitle!: 'connections'
  @Prop({ required: true }) public name!: string
  @Prop() public clickMethod!: <T>() => T | void

  @Getter('currentLang') private getterLang!: Language

  get imageSrc(): string {
    return require(`../assets/images/${this.name}`)
  }

  get emqxCloudWebsite(): string {
    return gaCustomLinks(this.getterLang).empty.EMQXCloud
  }
}
</script>

<style lang="scss" scoped>
.empty-page {
  .empty-page__block {
    .primary-btn {
      background: linear-gradient(134deg, #37dc85 0%, #35ca8d 100%);
      color: var(--color-text-active);
      border: 1px solid #37dc85;
    }
    img {
      margin-bottom: 20px;
    }
    text-align: center;
    padding-top: 30%;
    p {
      margin: 32px auto;
      max-width: 650px;
    }
  }
}
</style>
