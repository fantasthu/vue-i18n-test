<template>
  <div>
    <template>
      <div>
        <el-card class="box-card" style="margin-top:40px;">
          <div slot="header" class="clearfix">
            <svg-icon icon-class="international" />
            <span style="margin-left:10px;">{{ $t('index_1') }}</span>
          </div>
          <div>
            <el-radio-group v-model="lang" size="small">
              <el-radio label="zh" border>{{ $t('index_2') }}</el-radio>
              <el-radio label="en" border>{{ $t('index_3') }}</el-radio>
              <el-radio label="es" border>{{ $t('index_4') }}</el-radio>
            </el-radio-group>
            <el-tag style="margin-top:15px;display:block;" type="info">{{ $t('index_5') }}</el-tag>
          </div>
          <div>
            <div class="block" style="margin-top:10px">
              <el-button class="item-btn" size="small">{{ $t('index_6') }}</el-button>
              <el-button class="item-btn" size="small" type="primary">{{ $t('index_7') }}</el-button>
              <el-button class="item-btn" size="small" type="success">{{ $t('index_8') }}</el-button>
              <el-button class="item-btn" size="small" type="info">{{ $t('index_9') }}</el-button>
              <el-button class="item-btn" size="small" type="warning">{{ $t('index_10') }}</el-button>
              <el-button class="item-btn" size="small" type="danger">{{ $t('index_11') }}</el-button>
            </div>
          </div>
        </el-card>
      </div>
    </template>
  </div>
</template>

<script>
const viewName = 'i18nView'

export default {
  name: 'I18n',
  data() {
    return {
      date: '',
      tableData: [
        {
          date: '2016-05-03',
          name: this.$t('index_12'),
          address: this.$t('index_13')
        },
        {
          date: '2016-05-02',
          name: this.$t('index_14'),
          address: this.$t('index_15')
        },
        {
          date: '2016-05-04',
          name: this.$t('index_16'),
          address: this.$t('index_13')
        },
        {
          date: '2016-05-01',
          name: this.$t('index_17'),
          address: this.$t('index_18')
        }
      ]
    }
  }
}
</script>
