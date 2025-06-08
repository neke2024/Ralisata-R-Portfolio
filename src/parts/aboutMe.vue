<template>
    <section class="about-me" id="about">
        <!-- Arrière-plan animé -->
        <div class="bg-animation">
            <div class="floating-shapes">
                <div class="shape shape-1"></div>
                <div class="shape shape-2"></div>
                <div class="shape shape-3"></div>
                <div class="shape shape-4"></div>
            </div>
        </div>
    
        <div class="container">
            <!-- Titre de section -->
            <div class="section-header" ref="sectionHeader">
                <h2 class="section-title">À Propos de Moi</h2>
                <div class="title-underline"></div>
            </div>
    
            <div class="about-content">
                <!-- Profil avec photo -->
                <div class="profile-section" ref="profileSection">
                    <div class="profile-image-container">
                        <div class="image-glow"></div>
                        <img src="../assets/profile.jpg" alt="Mon profil" class="profile-image">
                        <div class="image-border"></div>
                    </div>
    
                    <div class="profile-info">
                        <h3 class="profile-name">Développeur Junior</h3>
                        <p class="profile-tagline">Passionné par l'innovation technologique</p>
    
                        <div class="social-links">
                            <a href="#" class="social-link" title="GitHub">
                                <i class="icon-github"></i>
                            </a>
                            <a href="#" class="social-link" title="LinkedIn">
                                <i class="icon-linkedin"></i>
                            </a>
                            <a href="#" class="social-link" title="Twitter">
                                <i class="icon-twitter"></i>
                            </a>
                        </div>
                    </div>
                </div>
    
                <!-- Description et compétences -->
                <div class="details-section" ref="detailsSection">
                    <div class="about-text">
                        <p class="intro-text">
                            Développeur junior passionné avec une soif d'apprendre et de créer des solutions innovantes.
                            Je maîtrise les technologies modernes et j'aime relever de nouveaux défis techniques.
                        </p>
    
                        <p class="description-text">
                            Mon parcours m'a permis d'acquérir une solide base en développement web, avec une approche
                            centrée sur l'expérience utilisateur et les bonnes pratiques. Je suis constamment à l'affût
                            des dernières tendances technologiques.
                        </p>
                    </div>
    
                    <!-- Compétences avec barres de progression -->
                    <div class="skills-container">
                        <h4 class="skills-title">Mes Compétences</h4>
                        <div class="skills-grid">
                            <div v-for="(skill, index) in skills" :key="skill.name" class="skill-item"
                                :style="{ animationDelay: `${index * 0.1}s` }" ref="skillItems">
                                <div class="skill-header">
                                    <span class="skill-name">{{ skill.name }}</span>
                                    <span class="skill-percentage">{{ skill.level }}%</span>
                                </div>
                                <div class="skill-bar">
                                    <div class="skill-progress"
                                        :style="{ width: animateSkills ? skill.level + '%' : '0%' }"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
    
            <!-- Stats -->
            <div class="stats-section" ref="statsSection">
                <div class="stats-grid">
                    <div v-for="(stat, index) in stats" :key="stat.label" class="stat-item"
                        :style="{ animationDelay: `${index * 0.2}s` }">
                        <div class="stat-number">{{ animateStats ? stat.value : 0 }}</div>
                        <div class="stat-label">{{ stat.label }}</div>
                        <div class="stat-glow"></div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
  name: "AboutMe",
  data() {
    return {
      animateSkills: false,
      animateStats: false,
      skills: [
        { name: "JavaScript", level: 85 },
        { name: "Vue.js", level: 80 },
        { name: "HTML/CSS", level: 90 },
        { name: "Python", level: 70 },
        { name: "JAVA", level: 75 },
        { name: "C", level: 65 }, { name: "PHP", level: 50 }
      ],
      stats: [
        { value: 50, label: "Projets Réalisés" },
        { value: 2, label: "Années d'Expérience" },
        { value: 15, label: "Technologies Maîtrisées" },
        { value: 100, label: "% Motivation" }
      ],
      observer: null
    }
  },
  mounted() {
    this.initScrollAnimations();
  },
  beforeUnmount() {
    if (this.observer) {
      this.observer.disconnect();
    }
  },
  methods: {
    initScrollAnimations() {
      // Intersection Observer pour animer au scroll
      this.observer = new IntersectionObserver((entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add('animate-in');

            // Animer les compétences
            if (entry.target === this.$refs.detailsSection) {
              setTimeout(() => {
                this.animateSkills = true;
              }, 500);
            }

            // Animer les stats
            if (entry.target === this.$refs.statsSection) {
              setTimeout(() => {
                this.animateStats = true;
                this.animateStatsNumbers();
              }, 300);
            }
          }
        });
      }, { threshold: 0.3 });

      // Observer les sections
      if (this.$refs.sectionHeader) this.observer.observe(this.$refs.sectionHeader);
      if (this.$refs.profileSection) this.observer.observe(this.$refs.profileSection);
      if (this.$refs.detailsSection) this.observer.observe(this.$refs.detailsSection);
      if (this.$refs.statsSection) this.observer.observe(this.$refs.statsSection);
    },

    animateStatsNumbers() {
      // Animation des chiffres qui comptent
      this.stats.forEach((stat, index) => {
        let current = 0;
        const increment = stat.value / 50;
        const timer = setInterval(() => {
          current += increment;
          if (current >= stat.value) {
            current = stat.value;
            clearInterval(timer);
          }
          this.stats[index].displayValue = Math.floor(current);
        }, 30);
      });
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Audiowide&family=Syncopate:wght@400;700&display=swap');

.about-me {
    position: relative;
    min-height: 100vh;
    background: linear-gradient(135deg, #0a0a0a 0%, #1a1a2e 50%, #16213e 100%);
    color: #ffffff;
    padding: 120px 0 80px;
    overflow: hidden;
}

/* Arrière-plan animé */
.bg-animation {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
}

.floating-shapes {
    position: absolute;
    width: 100%;
    height: 100%;
}

.shape {
    position: absolute;
    border: 1px solid rgba(0, 255, 255, 0.2);
    animation: float 8s ease-in-out infinite;
}

.shape-1 {
    width: 60px;
    height: 60px;
    top: 20%;
    left: 10%;
    border-radius: 50%;
    animation-delay: 0s;
}

.shape-2 {
    width: 40px;
    height: 40px;
    top: 60%;
    right: 15%;
    transform: rotate(45deg);
    animation-delay: 2s;
}

.shape-3 {
    width: 80px;
    height: 80px;
    bottom: 30%;
    left: 20%;
    border-radius: 20px;
    animation-delay: 4s;
}

.shape-4 {
    width: 50px;
    height: 50px;
    top: 40%;
    right: 30%;
    clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
    animation-delay: 6s;
}

@keyframes float {

    0%,
    100% {
        transform: translateY(0px) rotate(0deg);
        opacity: 0.3;
    }

    50% {
        transform: translateY(-30px) rotate(180deg);
        opacity: 0.8;
    }
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    position: relative;
    z-index: 10;
}

/* Titre de section */
.section-header {
    text-align: center;
    margin-bottom: 80px;
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.8s ease;
}

.section-header.animate-in {
    opacity: 1;
    transform: translateY(0);
}

.section-title {
    font-family: "Syncopate", sans-serif;
    font-size: clamp(2.5rem, 5vw, 4rem);
    font-weight: 700;
    margin-bottom: 20px;
    background: linear-gradient(45deg, #00ffff, #ff00ff);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

.title-underline {
    width: 100px;
    height: 3px;
    background: linear-gradient(90deg, #00ffff, #ff00ff);
    margin: 0 auto;
    border-radius: 2px;
}

/* Section profil */
.about-content {
    display: grid;
    grid-template-columns: 1fr 1.5fr;
    gap: 60px;
    margin-bottom: 80px;
}

.profile-section {
    opacity: 0;
    transform: translateX(-50px);
    transition: all 0.8s ease;
}

.profile-section.animate-in {
    opacity: 1;
    transform: translateX(0);
}

.profile-image-container {
    position: relative;
    width: 280px;
    height: 280px;
    margin: 0 auto 30px;
}

.image-glow {
    position: absolute;
    top: -10px;
    left: -10px;
    right: -10px;
    bottom: -10px;
    background: linear-gradient(45deg, #00ffff, #ff00ff, #00ffff);
    border-radius: 50%;
    animation: rotate 4s linear infinite;
    z-index: 1;
}

@keyframes rotate {
    0% {
        transform: rotate(0deg);
    }

    100% {
        transform: rotate(360deg);
    }
}

.profile-image {
    width: 100%;
    height: 100%;
    border-radius: 50%;
    object-fit: cover;
    position: relative;
    z-index: 2;
    border: 5px solid #0a0a0a;
}

.image-border {
    position: absolute;
    top: 5px;
    left: 5px;
    right: 5px;
    bottom: 5px;
    border: 2px solid rgba(0, 255, 255, 0.5);
    border-radius: 50%;
    z-index: 3;
}

.profile-info {
    text-align: center;
}

.profile-name {
    font-family: "Audiowide", sans-serif;
    font-size: 1.8rem;
    margin-bottom: 10px;
    color: #00ffff;
}

.profile-tagline {
    font-size: 1.1rem;
    color: rgba(255, 255, 255, 0.8);
    margin-bottom: 30px;
}

.social-links {
    display: flex;
    gap: 20px;
    justify-content: center;
}

.social-link {
    width: 50px;
    height: 50px;
    border: 2px solid rgba(0, 255, 255, 0.3);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #00ffff;
    text-decoration: none;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
}

.social-link::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 255, 255, 0.1);
    transform: scale(0);
    transition: transform 0.3s ease;
    border-radius: 50%;
}

.social-link:hover::before {
    transform: scale(1);
}

.social-link:hover {
    border-color: #00ffff;
    box-shadow: 0 0 20px rgba(0, 255, 255, 0.5);
    transform: translateY(-3px);
}

/* Section détails */
.details-section {
    opacity: 0;
    transform: translateX(50px);
    transition: all 0.8s ease;
}

.details-section.animate-in {
    opacity: 1;
    transform: translateX(0);
}

.about-text {
    margin-bottom: 40px;
}

.intro-text {
    font-size: 1.3rem;
    line-height: 1.6;
    margin-bottom: 20px;
    color: #ffffff;
}

.description-text {
    font-size: 1.1rem;
    line-height: 1.6;
    color: rgba(255, 255, 255, 0.8);
}

/* Compétences */
.skills-container {
    margin-top: 40px;
}

.skills-title {
    font-family: "Syncopate", sans-serif;
    font-size: 1.5rem;
    margin-bottom: 30px;
    color: #00ffff;
}

.skills-grid {
    display: grid;
    gap: 20px;
}

.skill-item {
    opacity: 0;
    animation: slideInRight 0.6s ease forwards;
}

@keyframes slideInRight {
    from {
        opacity: 0;
        transform: translateX(30px);
    }

    to {
        opacity: 1;
        transform: translateX(0);
    }
}

.skill-header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 8px;
}

.skill-name {
    font-weight: 600;
    color: #ffffff;
}

.skill-percentage {
    color: #00ffff;
    font-weight: 600;
}

.skill-bar {
    height: 8px;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 4px;
    overflow: hidden;
    position: relative;
}

.skill-progress {
    height: 100%;
    background: linear-gradient(90deg, #00ffff, #ff00ff);
    border-radius: 4px;
    transition: width 1.5s ease;
    position: relative;
}

.skill-progress::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
    animation: shine 2s ease-in-out infinite;
}

@keyframes shine {
    0% {
        transform: translateX(-100%);
    }

    100% {
        transform: translateX(100%);
    }
}

/* Section stats */
.stats-section {
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.8s ease;
}

.stats-section.animate-in {
    opacity: 1;
    transform: translateY(0);
}

.stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 30px;
}

.stat-item {
    text-align: center;
    padding: 30px 20px;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(0, 255, 255, 0.2);
    border-radius: 15px;
    position: relative;
    overflow: hidden;
    transition: all 0.3s ease;
    opacity: 0;
    animation: fadeInUp 0.6s ease forwards;
}

@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(30px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.stat-item:hover {
    transform: translateY(-5px);
    border-color: #00ffff;
    box-shadow: 0 10px 30px rgba(0, 255, 255, 0.3);
}

.stat-number {
    font-family: "Audiowide", sans-serif;
    font-size: 3rem;
    font-weight: bold;
    color: #00ffff;
    margin-bottom: 10px;
}

.stat-label {
    font-size: 1.1rem;
    color: rgba(255, 255, 255, 0.8);
    text-transform: uppercase;
    letter-spacing: 1px;
}

.stat-glow {
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(0, 255, 255, 0.1), transparent);
    transition: left 0.8s ease;
}

.stat-item:hover .stat-glow {
    left: 100%;
}

/* Icônes sociales (simulées avec CSS) */
.icon-github::before {
    content: "🐙";
}

.icon-linkedin::before {
    content: "💼";
}

.icon-twitter::before {
    content: "🐦";
}

/* Responsive */
@media (max-width: 768px) {
    .about-content {
        grid-template-columns: 1fr;
        gap: 40px;
    }

    .profile-image-container {
        width: 220px;
        height: 220px;
    }

    .stats-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 20px;
    }

    .section-title {
        font-size: 2rem;
    }
}

@media (max-width: 480px) {
    .about-me {
        padding: 100px 0 60px;
    }

    .stats-grid {
        grid-template-columns: 1fr;
    }

    .social-links {
        gap: 15px;
    }

    .social-link {
        width: 40px;
        height: 40px;
    }
}
</style>