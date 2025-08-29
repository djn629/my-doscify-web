# Headline

> An awesome project.
# 我的联系方式

<!-- 顶部功能区（仅保留访问统计和暗黑模式） -->
<div class="top-bar">
  <div class="visit-count">访问次数: <span id="visitCount">0</span></div>
  <!-- 新增：实时时间按钮（点击跳转北京时间官网） -->
  <a href="https://time.tianqi.com/" target="_blank" class="time-button" rel="noopener noreferrer" aria-label="查看北京时间官网">
    <i class="fa fa-clock-o"></i>
    <span id="liveTime"></span>
  </a>
  <button id="darkModeToggle" class="mode-toggle" aria-label="切换暗黑模式">
    <i class="fa fa-moon-o"></i>
    <span>暗黑模式</span>
  </button>
</div>

<div class="main-card">
  <h1 class="page-title">欢迎访问我的页面</h1>
  
  <!-- 联系模块 -->
  <section class="contact-section">
    <h2 class="section-title">
      <i class="fa fa-address-card-o"></i> 联系我
    </h2>
    <a href="https://qm.qq.com/cgi-bin/qm/qr?k=你的QQ密钥" 
       target="_blank" 
       class="qq-card" 
       rel="noopener noreferrer"
       aria-label="添加QQ好友（QQ号：2939884744）">
      <div class="qq-info">
        <i class="fa fa-qq text-3xl text-blue-500"></i>
        <div>
          <div class="qq-label">我的QQ</div>
          <div class="qq-number">2939884744</div>
        </div>
      </div>
      <img src="images/qq-qrcode.png" alt="QQ二维码（扫码添加好友）" class="qq-qrcode">
    </a>
    <p class="section-note">点击卡片或扫码可添加我为QQ好友（图片可能无法显示,所以请点击添加）</p>
  </section>

  <!-- 动态壁纸获取模块 -->
  <section class="wallpaper-section">
    <h2 class="section-title">
      <i class="fa fa-image"></i> 动态壁纸获取
    </h2>
    <a href="https://www.miyoushe.com/sr/collection/2244448" 
       target="_blank" 
       class="wallpaper-btn"
       rel="noopener noreferrer"
       aria-label="前往米游社获取动态壁纸">
      <i class="fa fa-download text-xl"></i>
      <span>点击获取动态壁纸（真）</span>
    </a>
    <p class="section-note">点击按钮跳转至米游社，获取官方合规动态壁纸</p>
  </section>

  <!-- 游戏资源推荐（大标题） -->
  <section class="game-resource-section">
    <h2 class="main-section-title">
      <i class="fa fa-gamepad"></i> 游戏资源推荐
    </h2>
    <a href="https://www.bilibili.com/video/BV1UT42167xb/?spm_id_from=333.337.search-card.all.click&vd_source=6b0f812b0c113ffdf51a6d1e5205ba0d" 
       target="_blank" 
       class="game-resource-btn"
       rel="noopener noreferrer"
       aria-label="查看B站游戏攻略视频">
      <i class="fa fa-play-circle-o text-xl"></i>
      <span>游戏技巧与合规攻略视频</span>
    </a>
    <p class="section-note">仅推荐合法游戏内容，请勿使用破坏公平性的工具</p>
  </section>

  <!-- 常用信息（大标题，仅保留一个复制按钮） -->
  <section class="info-section">
    <h2 class="main-section-title">
      <i class="fa fa-list-alt"></i> 常用信息
    </h2>
    <p class="section-desc">点击按钮复制内容，下方显示复制文本（支持电脑/手机）</p>
    
    <div class="info-container">
      <div class="copy-btn-list">
        <!-- 仅保留第一个复制按钮 -->
        <div class="copy-item">
          <button class="copy-btn" 
                  data-copy='getgenv().XiaoPi="皮脚本QQ群1002100032" loadstring(game:HttpGet("https://raw.githubusercontent.com/xiaopi77/xiaopi77/main/QQ1002100032-Roblox-Pi-script.lua"))()' 
                  aria-label="复制皮脚本内容"
                  data-id="copy1">
            <i class="fa fa-file-text-o"></i>
            <span>皮脚本（合规用途）</span>
          </button>
          <div class="copy-content" id="copyContent1" aria-live="polite"></div>
        </div>
      </div>
    </div>
  </section>
</div>

<!-- 返回顶部按钮 -->
<button id="backToTop" class="back-to-top" aria-label="返回顶部">
  <i class="fa fa-arrow-up"></i>
</button>

<!-- 功能脚本 -->
<script>
document.addEventListener('DOMContentLoaded', function() {
  const utils = {
    // 新增：实时时间按钮功能
    initLiveTime: function() {
      const timeElement = document.getElementById('liveTime');
      
      const updateLiveTime = () => {
        try {
          const now = new Date();
          const options = { 
            hour: '2-digit', minute: '2-digit', second: '2-digit'
          };
          timeElement.textContent = now.toLocaleTimeString('zh-CN', options);
        } catch (e) {
          console.error('时间更新失败:', e);
        }
      };
      
      // 初始化显示并每秒更新
      updateLiveTime();
      this.timeInterval = setInterval(updateLiveTime, 1000);
    },

    initVisitCount: function() {
      try {
        let count = localStorage.getItem('visitCount') || '0';
        count = parseInt(count, 10) + 1;
        localStorage.setItem('visitCount', count.toString());
        
        const countElement = document.getElementById('visitCount');
        const target = count;
        let current = parseInt(countElement.textContent, 10) || 0;
        const duration = 500;
        const steps = 30;
        const increment = (target - current) / steps;
        let step = 0;
        
        const updateCounter = () => {
          if (step >= steps) {
            countElement.textContent = target;
            return;
          }
          step++;
          current += increment;
          countElement.textContent = Math.round(current);
          requestAnimationFrame(updateCounter);
        };
        updateCounter();
      } catch (e) {
        console.error('访问统计失败:', e);
        document.getElementById('visitCount').textContent = '统计出错';
      }
    },

    showToast: function(message, type = 'info') {
      let toast = document.querySelector('.toast-notification');
      if (toast) toast.remove();
      
      toast = document.createElement('div');
      toast.className = `toast-notification toast-${type}`;
      toast.textContent = message;
      toast.setAttribute('role', 'alert');
      document.body.appendChild(toast);
      
      setTimeout(() => toast.classList.add('show'), 10);
      setTimeout(() => {
        toast.classList.remove('show');
        setTimeout(() => toast.remove(), 300);
      }, 2000);
    },

    initCopy: function() {
      const copyBtns = document.querySelectorAll('.copy-btn');
      copyBtns.forEach(btn => {
        btn.addEventListener('click', function() {
          try {
            const copyText = this.getAttribute('data-copy');
            const copyId = this.getAttribute('data-id');
            const contentElement = document.getElementById(`copyContent${copyId.replace('copy', '')}`);
            
            if (!copyText) {
              utils.showToast('没有可复制的内容', 'warning');
              return;
            }

            this.classList.add('copying');
            document.querySelectorAll('.copy-content').forEach(el => {
              if (el !== contentElement) el.classList.remove('show');
            });

            navigator.clipboard.writeText(copyText).then(() => {
              contentElement.textContent = copyText;
              contentElement.classList.add('show');
              const originalHTML = this.innerHTML;
              this.innerHTML = '<i class="fa fa-check text-green-500"></i><span>已复制！</span>';
              
              setTimeout(() => {
                this.innerHTML = originalHTML;
                this.classList.remove('copying');
              }, 1500);
              utils.showToast('复制成功！', 'success');
            }).catch(err => {
              console.error('复制失败:', err);
              const textarea = document.createElement('textarea');
              textarea.value = copyText;
              document.body.appendChild(textarea);
              textarea.select();
              document.execCommand('copy');
              document.body.removeChild(textarea);
              contentElement.textContent = copyText;
              contentElement.classList.add('show');
              this.classList.remove('copying');
              utils.showToast('已用备用方式复制', 'info');
            });
          } catch (e) {
            console.error('复制功能出错:', e);
            this.classList.remove('copying');
            utils.showToast('复制失败，请手动复制', 'error');
          }
        });
      });
    },

    initBackToTop: function() {
      const backToTopBtn = document.getElementById('backToTop');
      window.addEventListener('scroll', () => {
        backToTopBtn.classList.toggle('show', window.pageYOffset > 300);
      });
      
      backToTopBtn.addEventListener('click', () => {
        const scrollToTop = () => {
          const position = window.pageYOffset;
          if (position > 0) {
            requestAnimationFrame(scrollToTop);
            window.scrollTo(0, position - Math.max(30, position / 10));
          }
        };
        scrollToTop();
      });
    },

    initDarkMode: function() {
      const toggle = document.getElementById('darkModeToggle');
      const html = document.documentElement;
      
      const isDark = localStorage.getItem('darkMode') === 'true' || 
                    (!localStorage.getItem('darkMode') && window.matchMedia('(prefers-color-scheme: dark)').matches);
      
      if (isDark) {
        html.classList.add('dark-mode');
        utils.updateDarkModeUI(true);
      }
      
      toggle.addEventListener('click', () => {
        html.classList.toggle('dark-mode');
        const newDark = html.classList.contains('dark-mode');
        localStorage.setItem('darkMode', newDark.toString());
        utils.updateDarkModeUI(newDark);
      });
    },

    updateDarkModeUI: function(isDark) {
      const toggle = document.getElementById('darkModeToggle');
      const icon = toggle.querySelector('i');
      const text = toggle.querySelector('span');
      
      if (isDark) {
        icon.classList.replace('fa-moon-o', 'fa-sun-o');
        text.textContent = '亮色模式';
        toggle.setAttribute('aria-label', '切换亮色模式');
      } else {
        icon.classList.replace('fa-sun-o', 'fa-moon-o');
        text.textContent = '暗黑模式';
        toggle.setAttribute('aria-label', '切换暗黑模式');
      }
    },

    cleanup: function() {
      window.addEventListener('beforeunload', () => {
        if (this.timeInterval) clearInterval(this.timeInterval);
      });
    }
  };

  // 初始化所有功能
  utils.initLiveTime();    // 新增的实时时间功能
  utils.initVisitCount();
  utils.initCopy();
  utils.initBackToTop();
  utils.initDarkMode();
  utils.cleanup();
});
</script>

<!-- 样式 -->
<style>
:root {
  --primary: #4a6cf7;
  --primary-light: #6b85f8;
  --primary-dark: #3a5ce7;
  --green: #48bb78;
  --warning: #f6ad55;
  --error: #f56565;
  --info: #4299e1;
  --bg-light: rgba(255, 255, 255, 0.85);
  --bg-card: rgba(255, 255, 255, 0.95);
  --bg-item: rgba(255, 255, 255, 0.8);
  --text-primary: #333;
  --text-secondary: #666;
  --text-light: #999;
  --border: #e0e0e0;
  --shadow-light: 0 2px 5px rgba(0, 0, 0, 0.08);
  --shadow-medium: 0 4px 8px rgba(0, 0, 0, 0.12);
  --transition: all 0.3s ease;
  --radius: 8px;
}

.dark-mode {
  --bg-light: rgba(30, 30, 30, 0.85);
  --bg-card: rgba(40, 40, 40, 0.95);
  --bg-item: rgba(50, 50, 50, 0.8);
  --text-primary: #f0f0f0;
  --text-secondary: #ddd;
  --text-light: #bbb;
  --border: #555;
  --shadow-light: 0 2px 5px rgba(0, 0, 0, 0.3);
  --shadow-medium: 0 4px 8px rgba(0, 0, 0, 0.4);
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background-image: url('https://cn.bing.com/images/search?view=detailV2&ccid=Cu2isNhO&id=4E57354E653B796800C7F189BCAA97716D2E9A1A&thid=OIP.Cu2isNhO8oRFZYTR3Qn59AHaEK&mediaurl=https%3A%2F%2Fupload-bbs.miyoushe.com%2Fupload%2F2024%2F12%2F21%2F162891450%2F57959c67ceaa552574b68796d3eaf3b5_3114444962962416898.png%3Fx-oss-process%3Dimage%2Fresize%2Cs_600%2Fquality%2Cq_80%2Fauto-orient%2C0%2Finterlace%2C1%2Fformat%2Cpng&exph=600&expw=1067&q=%E5%B4%A9%E5%9D%8F%E6%98%9F%E7%A9%B9%E9%93%81%E9%81%93%E5%8A%A8%E6%80%81%E5%A3%81%E7%BA%B8&FORM=IRPRST&ck=74D5BC2DAB79DE038B35A970B1335954&selectedIndex=11&itb=0&cw=1145&ch=577&ajaxhist=0&ajaxserp=0');
  background-size: cover;
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
  position: relative;
  min-height: 100vh;
  color: var(--text-primary);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
}

body::before {
  content: "";
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: var(--bg-light);
  z-index: -1;
  transition: var(--transition);
}

.content {
  max-width: 1100px;
  margin: 0 auto;
  padding: 1rem;
}

.main-card {
  background-color: var(--bg-card);
  border-radius: var(--radius);
  padding: 2rem;
  margin-top: 1rem;
  box-shadow: var(--shadow-light);
  transition: var(--transition);
}

.top-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.8rem 1.2rem;
  background-color: var(--bg-card);
  border-radius: var(--radius);
  box-shadow: var(--shadow-light);
  flex-wrap: wrap;
  gap: 1rem;
}

.visit-count {
  color: var(--text-secondary);
  white-space: nowrap;
}

/* 新增：实时时间按钮样式 */
.time-button {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.4rem 0.8rem;
  background-color: var(--primary);
  color: white;
  border-radius: calc(var(--radius) / 2);
  text-decoration: none;
  font-weight: 500;
  transition: var(--transition);
  border: none;
  cursor: pointer;
  white-space: nowrap;
}

.time-button:hover {
  background-color: var(--primary-dark);
  transform: translateY(-2px);
  box-shadow: var(--shadow-light);
}

.mode-toggle {
  background: transparent;
  border: 1px solid var(--border);
  padding: 0.4rem 0.8rem;
  border-radius: calc(var(--radius) / 2);
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: var(--text-primary);
  transition: var(--transition);
}

.mode-toggle:hover {
  background-color: rgba(0, 0, 0, 0.05);
  border-color: var(--primary);
}

.page-title {
  text-align: center;
  margin-bottom: 2rem;
  color: var(--primary);
  font-weight: 700;
  font-size: 1.8rem;
  position: relative;
  padding-bottom: 0.8rem;
}

.page-title::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 3px;
  background-color: var(--primary);
  border-radius: 3px;
}

section {
  margin-bottom: 3rem;
  padding-bottom: 1.5rem;
  border-bottom: 1px solid var(--border);
}

section:last-of-type {
  border-bottom: none;
  margin-bottom: 1rem;
  padding-bottom: 0;
}

/* 普通标题样式 */
.section-title {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  margin-bottom: 1.2rem;
  color: var(--primary);
  font-size: 1.4rem;
  font-weight: 600;
}

/* 大标题样式 */
.main-section-title {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.8rem;
  color: var(--primary);
  font-size: 1.8rem;
  font-weight: 700;
  padding: 0.8rem 1.2rem;
  background-color: rgba(74, 108, 247, 0.1);
  border-radius: var(--radius);
  border-left: 4px solid var(--primary);
}

.main-section-title i {
  background-color: var(--primary);
  color: white;
  width: 45px;
  height: 45px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.dark-mode .main-section-title {
  background-color: rgba(74, 108, 247, 0.2);
}

.section-title i {
  background-color: var(--primary);
  color: white;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.section-note, .section-desc {
  color: var(--text-secondary);
  margin-top: 0.8rem;
  font-size: 0.95rem;
}

.qq-card {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  background-color: var(--bg-item);
  border-radius: var(--radius);
  padding: 1.2rem;
  text-decoration: none;
  color: var(--text-primary);
  transition: var(--transition);
  border: 1px solid var(--border);
  max-width: 600px;
}

.qq-card:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-medium);
  border-color: var(--primary-light);
}

.qq-info {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.qq-label {
  color: var(--text-secondary);
  font-size: 0.9rem;
}

.qq-number {
  font-size: 1.3rem;
  font-weight: 600;
}

.qq-qrcode {
  width: 90px;
  height: 90px;
  border-radius: calc(var(--radius) / 2);
  border: 2px solid var(--border);
  box-shadow: var(--shadow-light);
}

.wallpaper-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.8rem;
  padding: 1rem 1.8rem;
  background-color: var(--primary);
  color: white;
  border-radius: var(--radius);
  text-decoration: none;
  font-size: 1.1rem;
  font-weight: 500;
  transition: var(--transition);
  box-shadow: var(--shadow-light);
  margin-top: 0.5rem;
}

.wallpaper-btn:hover {
  background-color: var(--primary-dark);
  transform: translateY(-3px);
  box-shadow: var(--shadow-medium);
}

.wallpaper-btn i {
  background-color: rgba(255, 255, 255, 0.2);
  width: 32px;
  height: 32px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.game-resource-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.8rem;
  padding: 1rem 1.8rem;
  background-color: var(--primary);
  color: white;
  border-radius: var(--radius);
  text-decoration: none;
  font-size: 1.1rem;
  font-weight: 500;
  transition: var(--transition);
  box-shadow: var(--shadow-light);
  margin-top: 0.5rem;
}

.game-resource-btn:hover {
  background-color: var(--primary-dark);
  transform: translateY(-3px);
  box-shadow: var(--shadow-medium);
}

.game-resource-btn i {
  background-color: rgba(255, 255, 255, 0.2);
  width: 32px;
  height: 32px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.info-container {
  width: 100%;
}

.copy-btn-list {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
}

.copy-item {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.copy-btn {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  padding: 0.9rem 1.2rem;
  background-color: var(--bg-item);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  cursor: pointer;
  transition: var(--transition);
  text-align: left;
  color: var(--text-primary);
  width: 100%;
}

.copy-btn i {
  color: var(--primary);
  width: 24px;
  text-align: center;
}

.copy-btn:hover {
  border-color: var(--primary);
  background-color: rgba(74, 108, 247, 0.05);
}

.copy-btn.copying {
  transform: scale(0.99);
  opacity: 0.9;
}

.copy-content {
  padding: 0.8rem 1.2rem;
  background-color: rgba(74, 108, 247, 0.05);
  border: 1px dashed var(--primary-light);
  border-radius: var(--radius);
  color: var(--text-primary);
  font-size: 0.9rem;
  line-height: 1.5;
  white-space: pre-wrap;
  word-break: break-all;
  opacity: 0;
  height: 0;
  overflow: hidden;
  transition: var(--transition);
}

.copy-content.show {
  opacity: 1;
  height: auto;
  min-height: 40px;
}

.dark-mode .copy-content {
  background-color: rgba(74, 108, 247, 0.1);
}

.back-to-top {
  position: fixed;
  bottom: 2rem;
  right: 2rem;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: var(--primary);
  color: white;
  border: none;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  box-shadow: var(--shadow-medium);
  opacity: 0;
  visibility: hidden;
  transition: var(--transition);
  z-index: 100;
}

.back-to-top.show {
  opacity: 1;
  visibility: visible;
}

.back-to-top:hover {
  background-color: var(--primary-dark);
  transform: translateY(-5px) scale(1.05);
}

.toast-notification {
  position: fixed;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%) translateY(100px);
  padding: 0.8rem 1.5rem;
  border-radius: calc(var(--radius) / 2);
  color: white;
  z-index: 1000;
  transition: transform 0.3s ease;
  box-shadow: var(--shadow-medium);
}

.toast-notification.show {
  transform: translateX(-50%) translateY(0);
}

.toast-success { background-color: var(--green); }
.toast-warning { background-color: var(--warning); }
.toast-error { background-color: var(--error); }
.toast-info { background-color: var(--info); }

@media (max-width: 768px) {
  .main-card {
    padding: 1.5rem 1rem;
  }
  
  .top-bar {
    padding: 0.8rem;
    justify-content: flex-start;
  }
  
  .qq-card {
    flex-direction: column;
    text-align: center;
    padding: 1rem;
    width: 100%;
  }
  
  .qq-info {
    flex-direction: column;
  }
  
  .page-title {
    font-size: 1.5rem;
  }
  
  .main-section-title {
    font-size: 1.5rem;
    padding: 0.6rem 1rem;
  }
  
  .wallpaper-btn, .game-resource-btn {
    width: 100%;
    justify-content: center;
    padding: 0.9rem 1rem;
    font-size: 1rem;
  }
  
  .back-to-top {
    bottom: 1.5rem;
    right: 1.5rem;
    width: 45px;
    height: 45px;
  }
  
  .copy-content {
    font-size: 0.85rem;
  }
}

.fa {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
    
