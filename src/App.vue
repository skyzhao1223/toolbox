<template>
  <div id="toolbox">
    <page-header/>
    <page-content>
      <router-view/>
    </page-content>
    <page-footer/>
  </div>
</template>

<script>
import PageHeader from '@/components/PageHeader'
import PageContent from '@/components/PageContent'
import PageFooter from '@/components/PageFooter'
export default {
  name: 'app',
  components: {
    PageHeader, PageContent, PageFooter
  }
}
</script>

<style>
#toolbox {
  font-family: 'OpenSans', Helvetica, Arial, sans-serif;
}
html, body {
  font-size: 14px;
  margin: 0;
}
main {
  min-height: calc( 100vh - 126px );
  background: linear-gradient(180deg, #f2f7fa, #f8fafc);
  /* background-color: #f2f7fa; */
  padding: 66px 120px 0;
}
ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
textarea, input, pre {
  outline: none;
  border: 0;
}
a {
 text-decoration: none;
}
</style>
