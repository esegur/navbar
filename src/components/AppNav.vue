<template>
  <el-container >
    <el-header class="nav-header">
      <el-row>
        <el-col :span="6">
          <div class="flex element-bloq-center bg-gray " style="border-radius: 30px; width: 270px" >
             <img :width="55" :src="photo" class="border-radius">
             <span style="padding-left: 15px" class="text-dark-gray-1"> {{ name }}  </span> 
          </div>
        </el-col>
        <el-col :span="18">
          <el-menu
            :router="true"
            :default-active="$route.path"
            mode="horizontal"
            class="el-menu-demo border-none box-shadow"
            background-color="#262626"
            text-color="#fff"
            active-text-color="#ff5000">
            <el-menu-item
              class="nav-text item-padding"
              v-for="item in items"
              :key="item.title"
              :index="item.url"
              exact>{{ item.title }}
            </el-menu-item>
            <el-submenu index="2">
              <template slot="title">Más</template>
              <el-menu-item
                class="nav-text item-padding"
                v-for="nextItem in nextItems"
                :key="nextItem.title"
                :index="nextItem.url"
                @click="close(nextItem.title)"
                exact>{{ nextItem.title }}
              </el-menu-item>
            </el-submenu>
          </el-menu>
        </el-col>
      </el-row>
    </el-header>
  </el-container>
</template>
<script>
import firebase from 'firebase'

export default {
  name: 'AppNav',
  props: {
    msg: String
  },
  data () {
    return{
      //items visibles en el nav
      items:[
        { url: '/material', title: 'Materiales' },
        { url: '/programs', title: 'Programas' },
        { url: '/segments', title: 'Segmentos' },
      ],
      //items dentro de la opción más
      nextItems:[
        { url: '/contract', title: 'Contratos'},
        { url: '/review', title: 'Revisión'},
        { url: '/', title: 'Cerrar Sesión' }
      ],
    }
  },
  methods: {
    close(index) {
      if(index === 'Cerrar Sesión') {
        this.logOut()
      }
    },
    logOut() {
      firebase.auth().signOut();
    },
  },

}
</script>