<template>
  <div id="menu-bar">
    <el-row type="flex">
      <el-col :span="8">
        <el-menu class="header-menu" :unique-opened="true" mode="horizontal" router :default-active='$route.path'>
          <el-menu-item :index="'/performance/home'">
            {{ $t("i18n.home") }}
          </el-menu-item>

          <el-submenu v-permission="['test_manager','test_user','test_viewer']"
                      index="3" popper-class="submenu">
            <template v-slot:title>{{$t('commons.project')}}</template>
            <ms-recent-list :options="projectRecent"/>
            <el-divider/>
            <ms-show-all :index="'/performance/project'"/>
            <ms-create-button v-permission="['test_manager','test_user']"  :index="'/performance/project/create'" :title="$t('project.create')"/>
          </el-submenu>

          <el-submenu v-permission="['test_manager','test_user','test_viewer']"
                      index="4" popper-class="submenu">
            <template v-slot:title>{{$t('commons.test')}}</template>
            <ms-recent-list :options="testRecent"/>
            <el-divider/>
            <ms-show-all :index="'/performance/test'"/>
            <ms-create-button v-permission="['test_manager','test_user']" :index="'/performance/test/create'" :title="$t('load_test.create')"/>
          </el-submenu>

          <el-submenu v-permission="['test_manager','test_user','test_viewer']"
                      index="5" popper-class="submenu">
            <template v-slot:title>{{$t('commons.report')}}</template>
            <ms-recent-list :options="reportRecent"/>
            <el-divider/>
            <ms-show-all :index="'/performance/report'"/>
          </el-submenu>
        </el-menu>
      </el-col>
      <el-col :span="8">
        <el-row type="flex" justify="center">
          <ms-create-test :to="'/performance/test/create'"/>
        </el-row>
      </el-col>
      <el-col :span="8"/>
    </el-row>
  </div>
</template>

<script>

  import MsCreateTest from "../../common/head/CreateTest";
  import MsRecentList from "../../common/head/RecentList";
  import MsCreateButton from "../../common/head/CreateButton";
  import MsShowAll from "../../common/head/ShowAll";

  export default {
    name: "PerformanceHeaderMenus",
    components: {
      MsCreateButton,
      MsShowAll,
      MsRecentList,
      MsCreateTest
    },
    data() {
      return {
        projectRecent: {
          title: this.$t('project.recent'),
          url: "/project/recent/5",
          index(item) {
            return '/performance/test/' + item.id;
          },
          router(item) {
            return {name: 'perPlan', params: {projectId: item.id, projectName: item.name}}
          }
        },
        testRecent: {
          title: this.$t('load_test.recent'),
          url: "/performance/recent/5",
          index(item) {
            return '/performance/test/edit/' + item.id;
          },
          router(item) {
          }
        },
        reportRecent: {
          title: this.$t('report.recent'),
          url: "/performance/report/recent/5",
          showTime: true,
          index(item) {
            return '/performance/report/view/' + item.id;
          },
          router(item) {
          }
        }
      }
    },
  }

</script>

<style scoped>
  .el-divider--horizontal {
    margin: 0;
  }

  .el-menu.el-menu--horizontal {
    border-bottom: none;
  }

  #menu-bar {
    border-bottom: 1px solid #E6E6E6;
    background-color: #FFF;
  }
</style>
