<template>
    <div class="Header" :class="{ scrolled: isScrolled }">
        <div class="container">
            <div class="left">
                <img src="../assets/logo.png" alt="me logo">
            </div>
            <div class="right">
                <!-- Menu desktop -->
                <nav class="desktop-nav">
                    <ul>
                        <li><a href="#" class="nav-link">Begin</a></li>
                        <li><a href="#" class="nav-link">About Me</a></li>
                        <li><a href="#" class="nav-link">Contact-Me</a></li>
                    </ul>
                    <button type="button" class="cv-btn">
                        <span class="btn-text">Télécharger mon CV</span>
                        <span class="btn-glow"></span>
                    </button>
                </nav>
    
                <!-- Menu burger pour mobile -->
                <div class="menu-toggle" @click="toggleMobileMenu" :class="{ active: mobileMenuOpen }">
                    <span></span>
                    <span></span>
                    <span></span>
                </div>
            </div>
        </div>
    
        <!-- Menu mobile overlay -->
        <div class="mobile-menu" :class="{ active: mobileMenuOpen }" @click="closeMobileMenu">
            <div class="mobile-menu-content" @click.stop>
                <ul>
                    <li><a href="#" class="nav-link" @click="closeMobileMenu">Begin</a></li>
                    <li><a href="#" class="nav-link" @click="closeMobileMenu">About Me</a></li>
                    <li><a href="#" class="nav-link" @click="closeMobileMenu">Contact-Me</a></li>
                </ul>
                <button type="button" class="cv-btn" @click="closeMobileMenu">
                    <span class="btn-text">Télécharger mon CV</span>
                    <span class="btn-glow"></span>
                </button>
            </div>
        </div>
    
        <div class="header-glow"></div>
    </div>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      mobileMenuOpen: false,
      isScrolled: false
    }
  },
  methods: {
    toggleMobileMenu() {
      this.mobileMenuOpen = !this.mobileMenuOpen;

      // Empêcher le scroll du body quand le menu est ouvert
      if (this.mobileMenuOpen) {
        document.body.style.overflow = 'hidden';
      } else {
        document.body.style.overflow = 'auto';
      }
    },
    closeMobileMenu() {
      this.mobileMenuOpen = false;
      document.body.style.overflow = 'auto';
    },
    handleResize() {
      // Fermer le menu mobile si on redimensionne vers desktop
      if (window.innerWidth > 768 && this.mobileMenuOpen) {
        this.closeMobileMenu();
      }
    },
    handleScroll() {
      this.isScrolled = window.scrollY > 50;
    }
  },
  mounted() {
    window.addEventListener('resize', this.handleResize);
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.handleResize);
    window.removeEventListener('scroll', this.handleScroll);
    document.body.style.overflow = 'auto';
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Audiowide&family=Syncopate:wght@400;700&display=swap');

.Header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background: rgba(10, 10, 10, 0.95);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border-bottom: 1px solid rgba(0, 255, 255, 0.2);
    color: #fff;
    padding: 15px 20px;
    height: 80px;
    z-index: 1000;
    transition: all 0.3s ease;
}

.Header::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg,
            rgba(0, 255, 255, 0.1) 0%,
            rgba(255, 0, 255, 0.05) 50%,
            rgba(0, 255, 255, 0.1) 100%);
    opacity: 0;
    transition: opacity 0.3s ease;
    pointer-events: none;
}

.Header:hover::before {
    opacity: 1;
}

.Header.scrolled {
    background: rgba(5, 5, 5, 0.98);
    border-bottom-color: rgba(0, 255, 255, 0.4);
    backdrop-filter: blur(30px);
}

.header-glow {
    position: absolute;
    bottom: -2px;
    left: 0;
    width: 100%;
    height: 2px;
    background: linear-gradient(90deg,
            transparent 0%,
            #00ffff 25%,
            #ff00ff 50%,
            #00ffff 75%,
            transparent 100%);
    animation: glowMove 3s ease-in-out infinite;
}

@keyframes glowMove {

    0%,
    100% {
        transform: translateX(-100%);
        opacity: 0;
    }

    50% {
        transform: translateX(100%);
        opacity: 1;
    }
}

.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 100%;
    max-width: 1200px;
    margin: 0 auto;
}

.left {
    flex: 1;
    display: flex;
    align-items: center;
}

.right {
    flex: 2;
    display: flex;
    justify-content: flex-end;
    align-items: center;
}

.left img {
    height: 50px;
    width: auto;
    display: block;
    border-radius: 50%;
    border: 2px solid rgba(0, 255, 255, 0.3);
    padding: 5px;
    transition: all 0.3s ease;
    filter: drop-shadow(0 0 10px rgba(0, 255, 255, 0.3));
}

.left img:hover {
    border-color: #00ffff;
    filter: drop-shadow(0 0 20px rgba(0, 255, 255, 0.8));
    transform: scale(1.05);
}

.desktop-nav {
    display: flex;
    align-items: center;
    gap: 20px;
}

ul {
    list-style: none;
    display: flex;
    margin: 0;
    padding: 0;
    gap: 30px;
}

li {
    position: relative;
}

.nav-link {
    font-family: "Syncopate", sans-serif;
    color: rgba(255, 255, 255, 0.8);
    text-decoration: none;
    font-weight: 400;
    font-size: 0.9rem;
    letter-spacing: 1px;
    text-transform: uppercase;
    position: relative;
    padding: 10px 0;
    transition: all 0.3s ease;
}

.nav-link::before {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 0;
    height: 2px;
    background: linear-gradient(90deg, #00ffff, #ff00ff);
    transition: width 0.3s ease;
}

.nav-link::after {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 0;
    height: 0;
    background: rgba(0, 255, 255, 0.1);
    border-radius: 50%;
    transform: translate(-50%, -50%);
    transition: all 0.3s ease;
    z-index: -1;
}

.nav-link:hover {
    color: #ffffff;
    text-shadow: 0 0 10px rgba(0, 255, 255, 0.8);
}

.nav-link:hover::before {
    width: 100%;
}

.nav-link:hover::after {
    width: 100px;
    height: 40px;
}

.cv-btn {
    position: relative;
    background: transparent;
    color: #fff;
    border: 2px solid #00ffff;
    padding: 12px 25px;
    border-radius: 50px;
    cursor: pointer;
    font-family: "Audiowide", sans-serif;
    font-size: 0.9rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    transition: all 0.3s ease;
    overflow: hidden;
    box-shadow: 0 0 20px rgba(0, 255, 255, 0.3);
}

.btn-text {
    position: relative;
    z-index: 2;
}

.btn-glow {
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg,
            transparent,
            rgba(0, 255, 255, 0.4),
            transparent);
    transition: left 0.6s ease;
}

.cv-btn:hover {
    background: rgba(0, 255, 255, 0.1);
    border-color: #ff00ff;
    box-shadow: 0 0 40px rgba(0, 255, 255, 0.6);
    transform: translateY(-2px);
    color: #ffffff;
}

.cv-btn:hover .btn-glow {
    left: 100%;
}

.cv-btn:active {
    transform: translateY(0);
}

/* Menu burger pour mobile */
.menu-toggle {
    display: none;
    flex-direction: column;
    cursor: pointer;
    padding: 5px;
    z-index: 1001;
}

.menu-toggle span {
    display: block;
    width: 25px;
    height: 3px;
    background: #00ffff;
    margin: 3px 0;
    transition: all 0.3s ease;
    box-shadow: 0 0 5px rgba(0, 255, 255, 0.5);
}

.menu-toggle.active span:nth-child(1) {
    transform: rotate(45deg) translate(5px, 5px);
    background: #ff00ff;
}

.menu-toggle.active span:nth-child(2) {
    opacity: 0;
}

.menu-toggle.active span:nth-child(3) {
    transform: rotate(-45deg) translate(7px, -6px);
    background: #ff00ff;
}

/* Mobile menu overlay */
.mobile-menu {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: rgba(5, 5, 5, 0.98);
    backdrop-filter: blur(20px);
    transform: translateX(-100%);
    transition: transform 0.3s ease;
    z-index: 999;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.mobile-menu.active {
    transform: translateX(0);
}

.mobile-menu-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

.mobile-menu ul {
    flex-direction: column;
    gap: 30px;
    text-align: center;
    margin-bottom: 40px;
}

.mobile-menu .nav-link {
    font-size: 1.2rem;
    padding: 15px 0;
}

.mobile-menu .cv-btn {
    padding: 15px 30px;
    font-size: 1rem;
}

/* Responsive Design */
@media (max-width: 1024px) {
    .container {
        padding: 0 20px;
    }

    ul {
        gap: 20px;
    }

    .nav-link {
        font-size: 0.85rem;
    }

    .cv-btn {
        padding: 10px 20px;
        font-size: 0.85rem;
    }
}

@media (max-width: 768px) {
    .Header {
        padding: 15px 20px;
        height: 80px;
    }

    .menu-toggle {
        display: flex;
    }

    .desktop-nav {
        display: none;
    }

    .left img {
        height: 45px;
    }

    .container {
        justify-content: space-between;
    }

    .right {
        justify-content: flex-end;
        flex: none;
    }
}

@media (max-width: 480px) {
    .Header {
        padding: 12px 15px;
        height: 70px;
    }

    .left img {
        height: 40px;
    }

    .mobile-menu .nav-link {
        font-size: 1.1rem;
    }

    .mobile-menu .cv-btn {
        padding: 12px 25px;
        font-size: 0.9rem;
    }
}

@media (max-width: 360px) {
    .Header {
        padding: 10px 12px;
    }

    .left img {
        height: 35px;
    }

    .menu-toggle span {
        width: 22px;
        height: 2px;
    }

    .mobile-menu ul {
        gap: 25px;
    }

    .mobile-menu .nav-link {
        font-size: 1rem;
    }
}
</style>