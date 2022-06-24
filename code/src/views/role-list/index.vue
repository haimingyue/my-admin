<template>
  <div class="">
    <el-card>
      <el-table :data="allRoles" border style="width: 100%">
        <el-table-column :label="$t('msg.role.index')" type="index" width="120">
        </el-table-column>
        <el-table-column :label="$t('msg.role.name')" prop="title">
        </el-table-column>
        <el-table-column :label="$t('msg.role.desc')" prop="describe">
        </el-table-column>
        <el-table-column
          :label="$t('msg.role.action')"
          prop="action"
          width="260"
          #default="{ row }"
        >
          <el-button
            type="primary"
            size="mini"
            @click="onDistributePermissionClick(row)"
            v-permission="['distributePermission']"
          >
            {{ $t('msg.role.assignPermissions') }}
          </el-button>
        </el-table-column>
      </el-table>
    </el-card>

    <distribute-permission
      v-model="distributePermissionVisible"
      :roleId="selectRoleId"
    ></distribute-permission>
  </div>
</template>

<script setup>
import { roleList } from '@/api/role'
import { watchSwitchLang } from '@/utils/i18n'
import { ref } from 'vue'
import DistributePermission from './components/DistributePermission.vue'

const allRoles = ref([])
const getRoleList = async () => {
  allRoles.value = [
            {
                "role":[
                    {
                        "id":"1",
                        "title":"超级管理员"
                    }
                ],
                "_id":"612710a0ec87aa543c9c341d",
                "id":"0",
                "openTime":"1433088000000",
                "username":"super-admin",
                "mobile":"188xxxx0001",
                "avatar":"https://m.imooc.com/static/wap/static/common/img/logo-small@2x.png"
            },
            {
                "role":[
                    {
                        "id":"2",
                        "title":"管理员"
                    }
                ],
                "_id":"612710a0ec87aa543c9c341e",
                "id":"1",
                "username":"admin",
                "openTime":"1559318400000",
                "mobile":"188xxxx0002",
                "avatar":"https://img4.sycdn.imooc.com/61110c2b0001152907400741-140-140.jpg"
            }
        ]
}
getRoleList()
watchSwitchLang(getRoleList)

/**
 * 分配权限
 */
const distributePermissionVisible = ref(false)
const selectRoleId = ref('')
const onDistributePermissionClick = row => {
  selectRoleId.value = row.id
  distributePermissionVisible.value = true
}
</script>
