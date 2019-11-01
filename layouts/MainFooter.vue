<template>
  <div>
    <footer class="footer">
      <div class="container">
        <nav>
          <ul>
            <li>
              <a href="#">
                About
              </a>
            </li>
            <li>
              <a href="#">
                Terms
              </a>
            </li>
            <li>
              <a href="#">
                Settings
              </a>
            </li>
          </ul>
        </nav>
        <div class="copyright">Hebrew-English Bible &copy; {{ year }}</div>
      </div>
    </footer>
  </div>
</template>
<script>
export default {
  name: 'MainFooter',
  data() {
    return {
      year: new Date().getFullYear()
    }
  }
}
</script>
<style></style>
