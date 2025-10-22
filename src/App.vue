<template>
  <div class="page">
    <header class="header">
      <nav class="nav">
        <div class="logo">
          <img src="/porsche-wordmark.svg" alt="Porsche Wordmark" />
          <span class="logo-text">SPARK</span>
        </div>
        <div class="nav-right">
          <ul class="nav-links">
            <li v-for="link in navLinks" :key="link.target">
              <a :href="`#${link.target}`">{{ link.label }}</a>
            </li>
          </ul>
          <button class="theme-toggle" type="button" @click="toggleTheme">
            {{ themeLabel }}
          </button>
        </div>
      </nav>
    </header>

    <main>
      <section class="hero">
        <div class="hero-bg"></div>
        <div class="hero-bg-car"></div>
        <div class="hero-content">
          <h1 class="hero-title">S P A R K</h1>
          <p class="hero-subtitle">主动、出人意料和个性化</p>
          <p class="hero-description">以人性化的方式采取积极主动的态度</p>
          <a href="#courses" class="cta-button">开始学习</a>
        </div>
      </section>

      <section class="philosophy-section" id="philosophy">
        <div class="philosophy-container">
          <h2 class="philosophy-title">SPARK 核心理念</h2>
          <div class="philosophy-grid">
            <article
              v-for="card in philosophyCards"
              :key="card.title"
              class="philosophy-card reveal-on-scroll"
            >
              <h3 class="philosophy-card-title">{{ card.title }}</h3>
              <p class="philosophy-card-desc">{{ card.description }}</p>
            </article>
          </div>
        </div>
      </section>

      <section class="courses-section" id="courses">
        <div class="section-header">
          <h2 class="section-title">五大核心模块</h2>
          <p class="section-subtitle">全面提升销售技能与客户服务能力</p>
        </div>

        <div class="courses-grid">
          <article
            v-for="course in courses"
            :key="course.id"
            class="course-card reveal-on-scroll"
            @click="openModal(course.id)"
          >
            <div class="course-letter">{{ course.letter }}</div>
            <div class="course-number">{{ course.number }}</div>
            <h3 class="course-title">{{ course.title }}</h3>
            <p class="course-description">{{ course.description }}</p>
            <div class="course-topics">
              <span
                v-for="topic in course.topicTags"
                :key="topic"
                class="topic-tag"
              >
                {{ topic }}
              </span>
            </div>
          </article>
        </div>
      </section>
    </main>

    <footer class="footer" id="contact">
      <div class="footer-logo">
        <img src="/porsche-wordmark.svg" alt="Porsche Wordmark" />
      </div>
      <p class="footer-text">© 2025 Porsche. All rights reserved.</p>
    </footer>

    <div
      class="modal"
      :class="{ active: isModalOpen }"
      role="dialog"
      aria-modal="true"
      aria-labelledby="modalTitle"
      aria-describedby="modalDescription"
      @click.self="closeModal"
    >
      <div v-if="activeCourse" class="modal-content">
        <button class="modal-close" type="button" @click="closeModal">
          <span aria-hidden="true">&times;</span>
          <span class="sr-only">关闭</span>
        </button>

        <div class="modal-letter">{{ activeCourse.letter }}</div>
        <h2 id="modalTitle" class="modal-title">{{ activeCourse.title }}</h2>
        <p id="modalDescription" class="modal-description">
          {{ activeCourse.description }}
        </p>

        <div class="modal-topics">
          <h3 class="topic-section-title">课程主题</h3>
          <article
            v-for="topic in activeCourse.topics"
            :key="topic.title"
            class="topic-item"
          >
            <h4 class="topic-item-title">{{ topic.title }}</h4>
            <p class="topic-item-description">{{ topic.description }}</p>
          </article>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount, watch } from 'vue';

const navLinks = [
  { label: '核心理念', target: 'philosophy' },
  { label: '课程模块', target: 'courses' },
  { label: '联系我们', target: 'contact' },
];

const theme = ref('dark');

const themeLabel = computed(() =>
  theme.value === 'dark' ? '浅色主题' : '深色主题',
);

const toggleTheme = () => {
  theme.value = theme.value === 'dark' ? 'light' : 'dark';
};

const philosophyCards = [
  {
    title: '主动出击',
    description:
      '以人性化的方式采取积极主动的态度，在客户需求出现之前就已经准备好解决方案。',
  },
  {
    title: '出人意料',
    description:
      '出人意料地推动和推销你的关注，让客户感受到超越期待的服务体验。',
  },
  {
    title: '个性化服务',
    description:
      '基于客户知识的个性化服务，用非个人化的触摸激活新客户关系。',
  },
];

const courses = [
  {
    id: 'courseS',
    letter: 'S',
    number: 'SPARK MODULE 01',
    title: '让它与众不同',
    description:
      '使我们的销售方式独特化，建立与客户的深度连接，创造差异化价值。',
    topicTags: ['使我的销售独特', '万能模型', '故障诊断-位置感', '建立关系与基础'],
    topics: [
      {
        title: '使我的销售独特',
        description:
          '打造独一无二的销售方式，用差异化的服务赢得客户的信赖与青睐。',
      },
      {
        title: '万能模型',
        description:
          '掌握通用模型，灵活应用在不同客户场景中，提升沟通效率与成功率。',
      },
      {
        title: '故障诊断-位置感',
        description:
          '精准识别客户痛点，快速定位问题所在，提供针对性的解决方案。',
      },
      {
        title: '建立关系与基础',
        description:
          '通过真诚互动与专业表现，建立与客户之间稳固的信任关系。',
      },
    ],
  },
  {
    id: 'courseP',
    letter: 'P',
    number: 'SPARK MODULE 02',
    title: '积极投入',
    description:
      '以个性化的方式采取积极主动，注重细节，与客户建立真诚的连接。',
    topicTags: ['以个性化方式开展销售', '以客户的方式沟通', '注重细节', '主动搭建桥梁'],
    topics: [
      {
        title: '以个性化方式开展销售',
        description:
          '针对不同客户的个性需求量身定制销售策略，打造专属体验。',
      },
      {
        title: '以客户的方式沟通',
        description: '站在客户角度思考，用他们习惯的方式交流，增强沟通效率。',
      },
      {
        title: '注重细节',
        description: '关注每一个细节，从小处见真章，让客户感受到专业与用心。',
      },
      {
        title: '主动搭建桥梁',
        description:
          '积极主动地搭建与客户的沟通桥梁，创造更多互动与连接的机会。',
      },
    ],
  },
  {
    id: 'courseA',
    letter: 'A',
    number: 'SPARK MODULE 03',
    title: '请保持善于倾听',
    description:
      '真诚倾听客户需求，理解商品结构的融合与差距，让客户做出最佳决策。',
    topicTags: [
      '真诚去倾听的需求',
      '让其他人做出你想做到的决定',
      '了解与商品结构的融合和差距',
      '让每个问题都得到重视',
    ],
    topics: [
      {
        title: '真诚去倾听的需求',
        description:
          '不仅听客户说什么，更要理解他们为什么这么说，挖掘真实需求。',
      },
      {
        title: '让其他人做出你想做到的决定',
        description:
          '通过巧妙的引导和专业的建议，帮助客户自主做出最佳决策。',
      },
      {
        title: '了解与商品结构的融合和差距',
        description:
          '深入理解产品组合，识别客户需求与产品功能之间的契合点与差距。',
      },
      {
        title: '让每个问题都得到重视',
        description: '认真对待客户的每一个疑问，提供详尽而专业的解答。',
      },
    ],
  },
  {
    id: 'courseR',
    letter: 'R',
    number: 'SPARK MODULE 04',
    title: '取样意识',
    description:
      '准确诊断客户状况，展现专业顾问价值，通过充分准备赢得客户信任。',
    topicTags: ['故障诊断', '为客户展现获得建议的价值', '做好准备', '成为客户心中的专家'],
    topics: [
      {
        title: '故障诊断',
        description: '快速准确地识别客户痛点，提供针对性的解决方案。',
      },
      {
        title: '为客户展现获得建议的价值',
        description:
          '让客户清晰感知到专业建议的价值，建立顾问式销售关系。',
      },
      {
        title: '做好准备',
        description:
          '在每次客户互动前做好充分准备，展现专业性与对客户的重视。',
      },
      {
        title: '成为客户心中的专家',
        description: '通过持续的专业表现，在客户心中建立专家形象。',
      },
    ],
  },
  {
    id: 'courseK',
    letter: 'K',
    number: 'SPARK MODULE 05',
    title: '展现意愿',
    description:
      '用行动展现服务意愿，成为客户心目中的顾客之星，建立长期的信任与合作关系。',
    topicTags: ['成为客户心中的顾客之星', '服务意愿的展现', '建立长期信任关系', '持续创造价值'],
    topics: [
      {
        title: '成为客户心中的顾客之星',
        description:
          '超越客户期待，提供卓越服务，成为客户心中不可替代的销售顾问。',
      },
      {
        title: '服务意愿的展现',
        description:
          '通过实际行动展现服务意愿，让客户感受到真诚与热情。',
      },
      {
        title: '建立长期信任关系',
        description:
          '从交易关系升华到信任关系，建立长期稳固的客户联系。',
      },
      {
        title: '持续创造价值',
        description:
          '在售前、售中、售后全过程中持续为客户创造价值。',
      },
    ],
  },
];

const activeCourseId = ref(null);

const isModalOpen = computed(() => activeCourseId.value !== null);
const activeCourse = computed(
  () => courses.find((course) => course.id === activeCourseId.value) ?? null,
);

const openModal = (courseId) => {
  activeCourseId.value = courseId;
};

const closeModal = () => {
  activeCourseId.value = null;
};

const handleKeydown = (event) => {
  if (event.key === 'Escape') {
    closeModal();
  }
};

let revealObserver;

const applyTheme = (value) => {
  const bodyClassList = document.body.classList;
  bodyClassList.remove('theme-dark', 'theme-light');
  bodyClassList.add(value === 'light' ? 'theme-light' : 'theme-dark');
};

onMounted(() => {
  window.addEventListener('keydown', handleKeydown);

  applyTheme(theme.value);

  revealObserver = new IntersectionObserver(
    (entries, observer) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible');
          observer.unobserve(entry.target);
        }
      });
    },
    {
      threshold: 0.15,
    },
  );

  document.querySelectorAll('.reveal-on-scroll').forEach((element) => {
    element.classList.add('reveal-init');
    revealObserver.observe(element);
  });
});

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown);
  if (revealObserver) {
    revealObserver.disconnect();
  }
  document.body.classList.remove('theme-dark', 'theme-light');
  document.body.style.overflow = '';
});

watch(isModalOpen, (open) => {
  document.body.style.overflow = open ? 'hidden' : '';
});

watch(theme, (value) => {
  applyTheme(value);
});
</script>

<style>
:root {
  --porsche-accent: #d5001c;
  --porsche-gold: #c9a75e;
  --motion-short: 0.25s;
  --motion-medium: 0.5s;
  --motion-long: 0.8s;
}

html {
  scroll-behavior: smooth;
}

body {
  --body-background: #0e0e12;
  --text-primary: #fbfcff;
  --text-secondary: rgba(251, 252, 255, 0.7);
  --text-tertiary: rgba(251, 252, 255, 0.6);
  --header-background: rgba(14, 14, 18, 0.95);
  --header-border: rgba(251, 252, 255, 0.1);
  --footer-background: #0e0e12;
  --footer-border: rgba(251, 252, 255, 0.1);
  --footer-text-color: rgba(251, 252, 255, 0.5);
  --surface-muted: rgba(14, 14, 18, 0.6);
  --surface-card: #2a2a2e;
  --surface-highlight: rgba(14, 14, 18, 0.5);
  --section-gradient-start: #0e0e12;
  --section-gradient-end: #2a2a2e;
  --course-section-before-opacity: 0.02;
  --hero-gradient-start: rgba(14, 14, 18, 0.7);
  --hero-gradient-end: rgba(14, 14, 18, 0.9);
  --hero-logo-filter: brightness(0) invert(1);
  --hero-logo-opacity: 0.03;
  --hero-car-final-opacity: 0.15;
  --logo-filter: brightness(0) invert(1);
  --nav-link-color: #fbfcff;
  --nav-link-hover: #d5001c;
  --card-border: rgba(251, 252, 255, 0.1);
  --course-card-border: rgba(251, 252, 255, 0.1);
  --card-border-hover: rgba(251, 252, 255, 0.3);
  --card-shadow: rgba(0, 0, 0, 0.5);
  --course-card-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
  --modal-backdrop: rgba(14, 14, 18, 0.8);
  --modal-background: rgba(14, 14, 18, 0.95);
  --modal-border: rgba(251, 252, 255, 0.1);
  --modal-close-color: rgba(251, 252, 255, 0.7);
  --topic-item-background: rgba(14, 14, 18, 0.5);
  --topic-item-hover-background: rgba(14, 14, 18, 0.8);
  --topic-tag-background: rgba(213, 0, 28, 0.1);
  --topic-tag-border: rgba(213, 0, 28, 0.3);
  --topic-tag-hover-background: rgba(213, 0, 28, 0.2);
  --topic-tag-hover-border: #d5001c;
  --scrollbar-track: #0e0e12;
  --scrollbar-thumb: #2a2a2e;
  --course-letter-opacity: 0.15;
  --theme-toggle-border: rgba(251, 252, 255, 0.4);
  --cta-shadow: rgba(213, 0, 28, 0.4);
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue',
    Arial, sans-serif;
  background-color: var(--body-background);
  color: var(--text-primary);
  line-height: 1.6;
  overflow-x: hidden;
  transition: background-color var(--motion-long), color var(--motion-short);
}

body.theme-dark {
  --body-background: #0e0e12;
  --text-primary: #fbfcff;
  --text-secondary: rgba(251, 252, 255, 0.7);
  --text-tertiary: rgba(251, 252, 255, 0.6);
  --header-background: rgba(14, 14, 18, 0.95);
  --header-border: rgba(251, 252, 255, 0.1);
  --footer-background: #0e0e12;
  --footer-border: rgba(251, 252, 255, 0.1);
  --footer-text-color: rgba(251, 252, 255, 0.5);
  --surface-muted: rgba(14, 14, 18, 0.6);
  --surface-card: #2a2a2e;
  --surface-highlight: rgba(14, 14, 18, 0.5);
  --section-gradient-start: #0e0e12;
  --section-gradient-end: #2a2a2e;
  --course-section-before-opacity: 0.02;
  --hero-gradient-start: rgba(14, 14, 18, 0.7);
  --hero-gradient-end: rgba(14, 14, 18, 0.9);
  --hero-logo-filter: brightness(0) invert(1);
  --hero-logo-opacity: 0.03;
  --hero-car-final-opacity: 0.15;
  --logo-filter: brightness(0) invert(1);
  --nav-link-color: #fbfcff;
  --nav-link-hover: #d5001c;
  --card-border: rgba(251, 252, 255, 0.1);
  --course-card-border: rgba(251, 252, 255, 0.1);
  --card-border-hover: rgba(251, 252, 255, 0.3);
  --card-shadow: rgba(0, 0, 0, 0.5);
  --course-card-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
  --modal-backdrop: rgba(14, 14, 18, 0.8);
  --modal-background: rgba(14, 14, 18, 0.95);
  --modal-border: rgba(251, 252, 255, 0.1);
  --modal-close-color: rgba(251, 252, 255, 0.7);
  --topic-item-background: rgba(14, 14, 18, 0.5);
  --topic-item-hover-background: rgba(14, 14, 18, 0.8);
  --topic-tag-background: rgba(213, 0, 28, 0.1);
  --topic-tag-border: rgba(213, 0, 28, 0.3);
  --topic-tag-hover-background: rgba(213, 0, 28, 0.2);
  --topic-tag-hover-border: #d5001c;
  --scrollbar-track: #0e0e12;
  --scrollbar-thumb: #2a2a2e;
  --course-letter-opacity: 0.15;
  --theme-toggle-border: rgba(251, 252, 255, 0.4);
  --cta-shadow: rgba(213, 0, 28, 0.4);
}

body.theme-light {
  --body-background: #f5f7fb;
  --text-primary: #0b1020;
  --text-secondary: rgba(11, 16, 32, 0.72);
  --text-tertiary: rgba(11, 16, 32, 0.55);
  --header-background: rgba(255, 255, 255, 0.78);
  --header-border: rgba(255, 255, 255, 0.4);
  --footer-background: rgba(244, 246, 252, 0.8);
  --footer-border: rgba(11, 16, 32, 0.08);
  --footer-text-color: rgba(11, 16, 32, 0.55);
  --surface-muted: rgba(255, 255, 255, 0.65);
  --surface-card: rgba(255, 255, 255, 0.55);
  --surface-highlight: rgba(255, 255, 255, 0.35);
  --section-gradient-start: rgba(248, 250, 255, 0.7);
  --section-gradient-end: rgba(226, 233, 247, 0.8);
  --course-section-before-opacity: 0.1;
  --hero-gradient-start: rgba(255, 255, 255, 0.6);
  --hero-gradient-end: rgba(233, 238, 248, 0.92);
  --hero-logo-filter: none;
  --hero-logo-opacity: 0.18;
  --hero-car-final-opacity: 0.32;
  --logo-filter: none;
  --nav-link-color: rgba(11, 16, 32, 0.82);
  --nav-link-hover: #d5001c;
  --card-border: rgba(255, 255, 255, 0.4);
  --course-card-border: rgba(255, 255, 255, 0.4);
  --card-border-hover: rgba(11, 16, 32, 0.18);
  --card-shadow: rgba(12, 22, 44, 0.12);
  --course-card-shadow: 0 25px 45px rgba(12, 22, 44, 0.12);
  --modal-backdrop: rgba(245, 247, 251, 0.65);
  --modal-background: rgba(255, 255, 255, 0.72);
  --modal-border: rgba(255, 255, 255, 0.55);
  --modal-close-color: rgba(11, 16, 32, 0.55);
  --topic-item-background: rgba(255, 255, 255, 0.6);
  --topic-item-hover-background: rgba(255, 255, 255, 0.9);
  --topic-tag-background: rgba(213, 0, 28, 0.09);
  --topic-tag-border: rgba(213, 0, 28, 0.22);
  --topic-tag-hover-background: rgba(213, 0, 28, 0.18);
  --topic-tag-hover-border: #d5001c;
  --scrollbar-track: rgba(244, 246, 252, 0.8);
  --scrollbar-thumb: rgba(196, 205, 220, 0.9);
  --course-letter-opacity: 0.09;
  --theme-toggle-border: rgba(11, 16, 32, 0.25);
  --cta-shadow: rgba(213, 0, 28, 0.18);
}

body.theme-light::before {
  content: '';
  position: fixed;
  inset: 0;
  z-index: -1;
  pointer-events: none;
  background:
    radial-gradient(at 12% 18%, rgba(255, 255, 255, 0.9), transparent 60%),
    radial-gradient(at 88% 12%, rgba(213, 223, 255, 0.7), transparent 55%),
    radial-gradient(at 52% 88%, rgba(236, 240, 255, 0.65), transparent 60%),
    linear-gradient(130deg, rgba(231, 236, 248, 0.85) 0%, rgba(255, 255, 255, 0.65) 40%, rgba(218, 226, 242, 0.88) 100%);
}

body.theme-light .header {
  box-shadow: 0 24px 48px rgba(12, 22, 44, 0.12);
}

body.theme-light .theme-toggle {
  background: rgba(255, 255, 255, 0.38);
  color: rgba(11, 16, 32, 0.75);
}

body.theme-light .theme-toggle:hover,
body.theme-light .theme-toggle:focus-visible {
  background: rgba(255, 255, 255, 0.6);
  color: rgba(11, 16, 32, 0.85);
}

body.theme-light .hero-description {
  color: rgba(11, 16, 32, 0.6);
}

body.theme-light .philosophy-card,
body.theme-light .course-card {
  box-shadow: 0 25px 55px rgba(12, 22, 44, 0.18);
}

body.theme-light .philosophy-card:hover,
body.theme-light .course-card:hover {
  box-shadow: 0 35px 68px rgba(12, 22, 44, 0.2);
}

body.theme-light .modal-content {
  box-shadow: 0 30px 80px rgba(12, 22, 44, 0.18);
}

body.theme-light .footer {
  backdrop-filter: blur(26px) saturate(155%);
}

body.theme-light .hero-bg::before {
  opacity: 0.12;
}

body.theme-light .hero-bg::after {
  opacity: 0.22;
}

.page {
  min-height: 100vh;
}

.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  padding: 0.5rem 2rem;
  background: var(--header-background);
  backdrop-filter: blur(10px);
  z-index: 1000;
  border-bottom: 1px solid var(--header-border);
  transition: background var(--motion-medium), border-color var(--motion-medium);
}

.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1600px;
  margin: 0 auto;
  gap: 2rem;
}

.logo {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.logo img {
  height: 3.8rem;
  width: auto;
  filter: var(--logo-filter);
  transition: transform var(--motion-medium), filter var(--motion-medium);
}

.logo img:hover {
  transform: scale(1.04);
}

.logo-text {
  font-size: 2.6rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  color: var(--text-primary);
  line-height: 1;
  transition: color var(--motion-medium);
}

.nav-right {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.nav-links {
  display: flex;
  gap: 2rem;
  list-style: none;
  align-items: center;
  margin: 0;
  padding: 0;
}

.nav-links a {
  color: var(--nav-link-color);
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 500;
  transition: color var(--motion-short), opacity var(--motion-short);
  letter-spacing: 0.05em;
}

.nav-links a:hover {
  color: var(--nav-link-hover);
}

.theme-toggle {
  border: 1px solid var(--theme-toggle-border);
  background: transparent;
  color: var(--nav-link-color);
  font-size: 0.78rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  padding: 0.5rem 1.4rem;
  border-radius: 999px;
  cursor: pointer;
  transition: all var(--motion-short);
  backdrop-filter: blur(14px) saturate(140%);
}

.theme-toggle:hover,
.theme-toggle:focus-visible {
  outline: none;
  background: var(--porsche-accent);
  border-color: var(--porsche-accent);
  color: #ffffff;
  box-shadow: 0 10px 24px rgba(213, 0, 28, 0.35);
}

.hero {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    135deg,
    var(--hero-gradient-start) 0%,
    var(--hero-gradient-end) 100%
  );
  transition: background var(--motion-long);
}

.hero-bg-car {
  position: absolute;
  bottom: -5%;
  right: -10%;
  width: 80%;
  height: 80%;
  background: url('/porsche-911.png') no-repeat left center;
  background-size: cover;
  background-position: left center;
  transform: translateX(150%);
  animation: carDriveIn 2.5s ease-out forwards;
  animation-delay: 0.5s;
  opacity: 0;
}

@keyframes carDriveIn {
  0% {
    transform: translateX(150%);
    opacity: 0;
  }
  100% {
    transform: translateX(0);
    opacity: var(--hero-car-final-opacity);
  }
}

.hero-bg::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 800px;
  height: 800px;
  background: radial-gradient(circle, var(--porsche-accent), transparent 70%);
  transform: translate(-50%, -50%);
  animation: pulse 4s ease-in-out infinite;
  opacity: 0.08;
}

.hero-bg::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 800px;
  height: 200px;
  background: url('/porsche-wordmark.svg') no-repeat center center;
  background-size: contain;
  transform: translate(-50%, -50%);
  opacity: var(--hero-logo-opacity);
  filter: var(--hero-logo-filter);
  transition: opacity var(--motion-medium), filter var(--motion-medium);
}

.hero-content {
  text-align: center;
  z-index: 2;
  max-width: 1000px;
  padding: 0 2rem;
}

.hero-title {
  font-size: clamp(4rem, 12vw, 8rem);
  font-weight: 700;
  letter-spacing: 0.3em;
  margin-bottom: 2rem;
  animation: fadeInUp var(--motion-long) ease-out;
}

.hero-subtitle {
  font-size: clamp(1.3rem, 2.5vw, 1.8rem);
  color: var(--text-secondary);
  margin-bottom: 1rem;
  letter-spacing: 0.05em;
  animation: fadeInUp var(--motion-long) ease-out 0.2s backwards;
}

.hero-description {
  font-size: clamp(1rem, 1.5vw, 1.2rem);
  color: var(--porsche-gold);
  margin-bottom: 3rem;
  letter-spacing: 0.03em;
  animation: fadeInUp var(--motion-long) ease-out 0.3s backwards;
}

.cta-button {
  display: inline-block;
  padding: 1.2rem 3.5rem;
  background-color: var(--porsche-accent);
  color: #ffffff;
  text-decoration: none;
  font-weight: 600;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  font-size: 0.9rem;
  transition: all var(--motion-medium);
  border: 2px solid var(--porsche-accent);
  animation: fadeInUp var(--motion-long) ease-out 0.4s backwards;
  box-shadow: 0 15px 40px var(--cta-shadow);
}

.cta-button:hover {
  background-color: transparent;
  color: var(--porsche-accent);
  transform: translateY(-3px);
}

.philosophy-section {
  padding: 8rem 3rem;
  background: linear-gradient(
    180deg,
    var(--section-gradient-start) 0%,
    var(--section-gradient-end) 100%
  );
  position: relative;
  overflow: hidden;
  transition: background var(--motion-medium);
}

.philosophy-section::before {
  content: '';
  position: absolute;
  bottom: 5%;
  right: 5%;
  width: 400px;
  height: 100px;
  background: url('/porsche-wordmark.svg') no-repeat center center;
  background-size: contain;
  opacity: var(--course-section-before-opacity);
  filter: var(--hero-logo-filter);
  transition: opacity var(--motion-medium), filter var(--motion-medium);
}

.philosophy-container {
  max-width: 1600px;
  margin: 0 auto;
}

.philosophy-title {
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 700;
  margin-bottom: 3rem;
  text-align: center;
  letter-spacing: 0.05em;
}

.philosophy-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2.5rem;
  margin-top: 4rem;
}

.philosophy-card {
  background: var(--surface-muted);
  border: 1px solid var(--card-border);
  padding: 3rem 2.5rem;
  text-align: center;
  transition: all var(--motion-medium);
  position: relative;
  overflow: hidden;
  backdrop-filter: blur(24px) saturate(160%);
}

.philosophy-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 3px;
  background: linear-gradient(90deg, var(--porsche-accent), var(--porsche-gold));
  transform: scaleX(0);
  transform-origin: left;
  transition: transform var(--motion-medium);
}

.philosophy-card:hover {
  transform: translateY(-8px);
  border-color: var(--card-border-hover);
  box-shadow: 0 25px 50px var(--card-shadow);
}

.philosophy-card:hover::before {
  transform: scaleX(1);
}

.philosophy-card-title {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: var(--porsche-gold);
}

.philosophy-card-desc {
  color: var(--text-secondary);
  line-height: 1.8;
}

.courses-section {
  padding: 8rem 3rem;
  max-width: 1600px;
  margin: 0 auto;
  position: relative;
}

.courses-section::before {
  content: '';
  position: absolute;
  top: 10%;
  left: -100px;
  width: 500px;
  height: 125px;
  background: url('/porsche-wordmark.svg') no-repeat center center;
  background-size: contain;
  opacity: var(--course-section-before-opacity);
  filter: var(--hero-logo-filter);
  transform: rotate(-15deg);
  transition: opacity var(--motion-medium), filter var(--motion-medium);
}

.section-header {
  text-align: center;
  margin-bottom: 5rem;
}

.section-title {
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 700;
  margin-bottom: 1.5rem;
  letter-spacing: 0.05em;
}

.section-subtitle {
  font-size: 1.3rem;
  color: var(--text-tertiary);
  letter-spacing: 0.03em;
}

.courses-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 2.5rem;
}

.course-card {
  background: var(--surface-card);
  border: 1px solid var(--course-card-border);
  padding: 3rem;
  transition: all var(--motion-medium);
  cursor: pointer;
  position: relative;
  overflow: hidden;
  backdrop-filter: blur(24px) saturate(160%);
}

.course-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 5px;
  background: var(--porsche-accent);
  transform: scaleX(0);
  transform-origin: left;
  transition: transform var(--motion-medium);
}

.course-card:hover {
  transform: translateY(-5px);
  border-color: var(--card-border-hover);
  box-shadow: var(--course-card-shadow);
}

.course-card:hover::before {
  transform: scaleX(1);
}

.course-letter {
  font-size: 5rem;
  font-weight: 700;
  color: var(--porsche-accent);
  opacity: var(--course-letter-opacity);
  position: absolute;
  top: 1rem;
  right: 2rem;
  line-height: 1;
}

.course-number {
  font-size: 0.85rem;
  color: var(--porsche-gold);
  letter-spacing: 0.15em;
  margin-bottom: 1rem;
  font-weight: 600;
}

.course-title {
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  letter-spacing: 0.02em;
  position: relative;
  z-index: 1;
}

.course-description {
  color: var(--text-secondary);
  margin-bottom: 2rem;
  line-height: 1.8;
  font-size: 1.05rem;
}

.course-topics {
  margin-top: 1.5rem;
}

.topic-tag {
  display: inline-block;
  padding: 0.5rem 1rem;
  background: var(--topic-tag-background);
  border: 1px solid var(--topic-tag-border);
  margin: 0.3rem;
  font-size: 0.85rem;
  color: var(--nav-link-color);
  transition: all var(--motion-short);
}

.topic-tag:hover {
  background: var(--topic-tag-hover-background);
  border-color: var(--topic-tag-hover-border);
}

.modal {
  position: fixed;
  inset: 0;
  background: var(--modal-backdrop);
  backdrop-filter: blur(6px);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  opacity: 0;
  visibility: hidden;
  transition: opacity var(--motion-medium), visibility var(--motion-medium);
  z-index: 2000;
}

.modal.active {
  opacity: 1;
  visibility: visible;
}

.modal-content {
  background: var(--modal-background);
  border: 1px solid var(--modal-border);
  max-width: 900px;
  width: 100%;
  padding: 3rem;
  position: relative;
  overflow-y: auto;
  max-height: 90vh;
  color: var(--text-primary);
  transition: background var(--motion-medium), border-color var(--motion-medium);
  backdrop-filter: blur(26px) saturate(170%);
}

.modal-close {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  background: transparent;
  border: none;
  color: var(--modal-close-color);
  font-size: 2rem;
  cursor: pointer;
  transition: color var(--motion-short);
}

.modal-close:hover {
  color: var(--porsche-accent);
}

.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}

.modal-letter {
  font-size: 8rem;
  font-weight: 700;
  color: var(--porsche-accent);
  opacity: var(--course-letter-opacity);
  line-height: 1;
  margin-bottom: 1rem;
}

.modal-title {
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 1rem;
}

.modal-description {
  font-size: 1.1rem;
  color: var(--text-secondary);
  line-height: 1.8;
}

.modal-topics {
  margin-top: 3rem;
}

.topic-section-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--porsche-gold);
  margin-bottom: 2rem;
  letter-spacing: 0.05em;
}

.topic-item {
  padding: 2rem;
  margin-bottom: 1.5rem;
  background: var(--topic-item-background);
  border-left: 4px solid var(--porsche-accent);
  transition: all var(--motion-short);
}

.topic-item:hover {
  background: var(--topic-item-hover-background);
  transform: translateX(10px);
  border-left-width: 6px;
}

.topic-item-title {
  font-size: 1.3rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.topic-item-description {
  color: var(--text-tertiary);
  font-size: 0.95rem;
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

@keyframes pulse {
  0%,
  100% {
    transform: translate(-50%, -50%) scale(1);
  }
  50% {
    transform: translate(-50%, -50%) scale(1.2);
  }
}

.footer {
  padding: 4rem 3rem 2rem;
  background: var(--footer-background);
  border-top: 1px solid var(--footer-border);
  text-align: center;
  transition: background var(--motion-medium), border-color var(--motion-medium);
}

.footer-logo {
  margin-bottom: 2rem;
}

.footer-logo img {
  height: 60px;
  width: auto;
  filter: var(--logo-filter);
  opacity: 0.7;
  transition: filter var(--motion-medium);
}

.footer-text {
  color: var(--footer-text-color);
  font-size: 0.9rem;
  letter-spacing: 0.05em;
}

::-webkit-scrollbar {
  width: 10px;
}

::-webkit-scrollbar-track {
  background: var(--scrollbar-track);
}

::-webkit-scrollbar-thumb {
  background: var(--scrollbar-thumb);
  border-radius: 5px;
  transition: background var(--motion-short);
}

::-webkit-scrollbar-thumb:hover {
  background: var(--porsche-accent);
}

.reveal-on-scroll.reveal-init {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s ease-out;
}

.reveal-on-scroll.is-visible {
  opacity: 1;
  transform: translateY(0);
}

@media (max-width: 1280px) {
  .nav {
    padding: 0 1rem;
  }
}

@media (max-width: 1024px) {
  .nav {
    flex-direction: column;
    align-items: flex-start;
    gap: 1rem;
  }

  .logo img {
    height: 3.2rem;
  }

  .logo-text {
    font-size: 2.3rem;
  }

  .nav-right {
    width: 100%;
    justify-content: space-between;
    flex-wrap: wrap;
  }

  .courses-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 768px) {
  .header {
    padding: 1rem 1.5rem;
  }

  .nav-right {
    flex-direction: column;
    align-items: stretch;
    gap: 1rem;
  }

  .nav-links {
    width: 100%;
    justify-content: center;
    gap: 1.5rem;
    font-size: 0.85rem;
    flex-wrap: wrap;
  }

  .theme-toggle {
    width: 100%;
    text-align: center;
  }

  .logo img {
    height: 2.8rem;
  }

  .logo-text {
    font-size: 2.1rem;
  }

  .courses-section,
  .philosophy-section {
    padding: 5rem 1.5rem;
  }

  .modal-content {
    padding: 2.5rem 1.5rem;
  }

  .modal-letter {
    font-size: 5rem;
  }
}
</style>
*** End Patch
