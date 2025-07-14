---
layout: home
title: 主页
---

<header class="site-header">
  <div class="wrapper">
  </div>
</header>
---
layout: home
---

<!-- 添加自定义样式 -->
<style>
  /* 移动端点击修复 */
  .post-list > li {
    position: relative;
    padding: 20px 0;
  }

  .post-list > li::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 1;
  }

  .post-link {
    position: relative;
    z-index: 2;
  }
</style>

<!-- 添加JavaScript -->
<script>
document.addEventListener('DOMContentLoaded', function() {
  if (/iPhone|iPad|iPod|Android/i.test(navigator.userAgent)) {
    document.querySelectorAll('.post-list > li').forEach(li => {
      li.onclick = function() {
        const link = this.querySelector('a');
        if(link) window.location = link.href;
      };
    });
  }
});
</script>

{{ content }} <!-- 保持原有内容 -->
