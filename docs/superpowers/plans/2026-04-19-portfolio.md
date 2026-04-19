# 개인 포트폴리오 정적 웹사이트 구현 계획

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 동기부여/기회제공 포트폴리오 정적 웹사이트를 단일 HTML 파일로 구축

**Architecture:** 단일 index.html 파일에 Tailwind CSS CDN을 사용하여 Hero+About, Services, Contact 세 섹션을 구현. 빌드 도구 없이 즉시 배포 가능.

**Tech Stack:** HTML5, Tailwind CSS (CDN), Pretendard 웹폰트

---

## 파일 구조

| 파일 | 역할 |
|------|------|
| `index.html` | 전체 페이지 - Hero, Services, Contact 섹션 포함 |

---

### Task 1: HTML 기본 구조 + Tailwind + Pretendard 폰트 설정

**Files:**
- Modify: `index.html`

- [ ] **Step 1: 기본 HTML 골격 작성**

index.html 전체를 다음 내용으로 교체:

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>포트폴리오 | 동기부여와 기회</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/static/pretendard.min.css">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            sans: ['Pretendard', 'sans-serif'],
          },
          colors: {
            accent: '#2563eb',
          }
        }
      }
    }
  </script>
  <style>
    html { scroll-behavior: smooth; }
  </style>
</head>
<body class="font-sans text-gray-900 bg-white">

  <!-- Navigation -->
  <!-- Hero + About -->
  <!-- Services -->
  <!-- Contact -->

</body>
</html>
```

- [ ] **Step 2: 브라우저에서 빈 페이지가 정상 로드되는지 확인**

- [ ] **Step 3: 커밋**

```bash
git add index.html
git commit -m "feat: add HTML skeleton with Tailwind and Pretendard font"
```

---

### Task 2: 네비게이션 바

**Files:**
- Modify: `index.html`

- [ ] **Step 1: 네비게이션 HTML 추가**

`<!-- Navigation -->` 주석을 다음으로 교체:

```html
  <nav id="navbar" class="fixed top-0 w-full z-50 transition-all duration-300 bg-transparent">
    <div class="max-w-6xl mx-auto px-6 py-4 flex justify-between items-center">
      <a href="#hero" class="text-xl font-bold">포트폴리오</a>
      <div class="hidden md:flex gap-8">
        <a href="#about" class="hover:text-accent transition">소개</a>
        <a href="#services" class="hover:text-accent transition">서비스</a>
        <a href="#contact" class="hover:text-accent transition">상담</a>
      </div>
      <button id="menu-btn" class="md:hidden text-2xl">&#9776;</button>
    </div>
    <div id="mobile-menu" class="hidden md:hidden px-6 pb-4">
      <a href="#about" class="block py-2 hover:text-accent transition">소개</a>
      <a href="#services" class="block py-2 hover:text-accent transition">서비스</a>
      <a href="#contact" class="block py-2 hover:text-accent transition">상담</a>
    </div>
  </nav>
```

- [ ] **Step 2: 스크롤 시 네비게이션 배경 변경 + 모바일 메뉴 토글 스크립트 추가**

`</body>` 태그 바로 앞에 추가:

```html
  <script>
    // Navbar scroll effect
    window.addEventListener('scroll', () => {
      const navbar = document.getElementById('navbar');
      if (window.scrollY > 50) {
        navbar.classList.add('bg-white', 'shadow-sm');
        navbar.classList.remove('bg-transparent');
      } else {
        navbar.classList.remove('bg-white', 'shadow-sm');
        navbar.classList.add('bg-transparent');
      }
    });

    // Mobile menu toggle
    document.getElementById('menu-btn').addEventListener('click', () => {
      document.getElementById('mobile-menu').classList.toggle('hidden');
    });

    // Close mobile menu on link click
    document.querySelectorAll('#mobile-menu a').forEach(link => {
      link.addEventListener('click', () => {
        document.getElementById('mobile-menu').classList.add('hidden');
      });
    });
  </script>
```

- [ ] **Step 3: 브라우저에서 네비게이션이 고정되고, 스크롤 시 배경이 변하는지 확인**

- [ ] **Step 4: 커밋**

```bash
git add index.html
git commit -m "feat: add fixed navbar with scroll effect and mobile menu"
```

---

### Task 3: Hero + About 섹션

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Hero + About HTML 추가**

`<!-- Hero + About -->` 주석을 다음으로 교체:

```html
  <!-- Hero -->
  <section id="hero" class="min-h-screen flex flex-col items-center justify-center text-center px-6">
    <h1 class="text-5xl md:text-7xl font-bold mb-6">동기부여와 기회를<br>제공합니다</h1>
    <p class="text-xl md:text-2xl text-gray-500 max-w-2xl mb-12">새로운 가능성을 발견하고, 변화를 만들어갑니다</p>
    <a href="#contact" class="bg-accent text-white px-8 py-4 rounded-lg text-lg font-semibold hover:bg-blue-700 transition">카카오톡으로 상담받기</a>
    <div class="mt-16 animate-bounce">
      <svg class="w-6 h-6 mx-auto text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3"/>
      </svg>
    </div>
  </section>

  <!-- About -->
  <section id="about" class="py-24 bg-gray-50">
    <div class="max-w-4xl mx-auto px-6 text-center">
      <h2 class="text-3xl md:text-4xl font-bold mb-8">소개</h2>
      <p class="text-lg text-gray-600 leading-relaxed max-w-3xl mx-auto">
        저는 사람들의 잠재력을 끌어내고, 새로운 기회를 연결하는 일을 합니다.
        동기부여를 통해 개인과 조직이 성장할 수 있도록 돕고,
        실질적인 기회를 제공하여 변화를 만들어갑니다.
      </p>
    </div>
  </section>
```

- [ ] **Step 2: 브라우저에서 Hero 전체 화면, 스크롤 시 About 섹션이 보이는지 확인**

- [ ] **Step 3: 커밋**

```bash
git add index.html
git commit -m "feat: add Hero and About sections"
```

---

### Task 4: Services 섹션

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Services HTML 추가**

`<!-- Services -->` 주석을 다음으로 교체:

```html
  <section id="services" class="py-24">
    <div class="max-w-6xl mx-auto px-6">
      <h2 class="text-3xl md:text-4xl font-bold text-center mb-16">서비스</h2>
      <div class="grid md:grid-cols-3 gap-8">
        <!-- Service Card 1 -->
        <div class="p-8 rounded-2xl border border-gray-200 hover:shadow-lg hover:-translate-y-1 transition-all duration-300">
          <div class="w-12 h-12 bg-blue-100 rounded-xl flex items-center justify-center text-accent text-2xl mb-6">&#127793;</div>
          <h3 class="text-xl font-bold mb-3">1:1 코칭</h3>
          <p class="text-gray-600">개인의 강점을 발견하고 목표를 설정하여 성장할 수 있도록 돕는 맞춤형 코칭</p>
        </div>
        <!-- Service Card 2 -->
        <div class="p-8 rounded-2xl border border-gray-200 hover:shadow-lg hover:-translate-y-1 transition-all duration-300">
          <div class="w-12 h-12 bg-blue-100 rounded-xl flex items-center justify-center text-accent text-2xl mb-6">&#128640;</div>
          <h3 class="text-xl font-bold mb-3">워크샵</h3>
          <p class="text-gray-600">팀과 조직의 동기부여를 위한 인터랙티브 워크샵 프로그램</p>
        </div>
        <!-- Service Card 3 -->
        <div class="p-8 rounded-2xl border border-gray-200 hover:shadow-lg hover:-translate-y-1 transition-all duration-300">
          <div class="w-12 h-12 bg-blue-100 rounded-xl flex items-center justify-center text-accent text-2xl mb-6">&#128218;</div>
          <h3 class="text-xl font-bold mb-3">콘텐츠</h3>
          <p class="text-gray-600">동기부여와 자기계발을 위한 지속적인 콘텐츠와 인사이트 제공</p>
        </div>
      </div>
    </div>
  </section>
```

- [ ] **Step 2: 브라우저에서 3개 카드가 반응형으로 표시되고, 호버 효과가 동작하는지 확인**

- [ ] **Step 3: 커밋**

```bash
git add index.html
git commit -m "feat: add Services section with card layout"
```

---

### Task 5: Contact (카카오톡 상담 CTA) 섹션 + Footer

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Contact 섹션 + Footer HTML 추가**

`<!-- Contact -->` 주석을 다음으로 교체:

```html
  <!-- Contact -->
  <section id="contact" class="py-24 bg-gray-50">
    <div class="max-w-4xl mx-auto px-6 text-center">
      <h2 class="text-3xl md:text-4xl font-bold mb-6">지금 카카오톡으로 상담받기</h2>
      <p class="text-lg text-gray-600 mb-12">궁금한 점이 있으신가요? 카카오톡으로 편하게 문의하세요</p>
      <a href="https://pf.kakao.com/_YOUR_CHANNEL_ID" target="_blank" rel="noopener noreferrer"
         class="inline-flex items-center gap-3 bg-[#FEE500] text-[#3C1E1E] px-10 py-5 rounded-xl text-xl font-bold hover:bg-[#FDD800] transition shadow-lg">
        <svg class="w-8 h-8" viewBox="0 0 24 24" fill="#3C1E1E">
          <path d="M12 3C6.48 3 2 6.58 2 11.03c0 2.76 1.81 5.19 4.58 6.65l-1.17 4.32 4.97-2.65c.53.05 1.07.08 1.62.08 5.52 0 10-3.58 10-8s-4.48-8-10-8v4.4c0 .24-.13.46-.35.58l-3.78 2.01.89-3.28c.06-.21-.01-.44-.18-.57C6.35 10.85 5.25 9.03 5.25 7.04c0-3.1 2.89-5.62 6.75-5.82V3z"/>
        </svg>
        카카오톡 상담하기
      </a>
    </div>
  </section>

  <!-- Footer -->
  <footer class="py-8 text-center text-gray-400 text-sm">
    <p>&copy; 2026 포트폴리오. All rights reserved.</p>
  </footer>
```

- [ ] **Step 2: 카카오톡 버튼의 `href`에서 `_YOUR_CHANNEL_ID`를 실제 카카오톡 채널 ID로 교체**

- [ ] **Step 3: 브라우저에서 카카오톡 버튼이 보이고, 클릭 시 링크가 동작하는지 확인**

- [ ] **Step 4: 커밋**

```bash
git add index.html
git commit -m "feat: add Contact CTA section and footer"
```

---

### Task 6: 전체 검증 + 최종 커밋

**Files:**
- Modify: `index.html` (최종 확인)

- [ ] **Step 1: 브라우저에서 전체 페이지 동작 확인**

체크리스트:
- [ ] 네비게이션 링크 클릭 시 해당 섹션으로 스무스 스크롤
- [ ] 스크롤 시 네비게이션 배경 변경
- [ ] 모바일 화면에서 햄버거 메뉴 동작
- [ ] Hero 섹션 전체 화면 높이
- [ ] 카카오톡 버튼 링크 정상 동작
- [ ] 반응형: 모바일/태블릿/데스크톱 레이아웃 정상

- [ ] **Step 2: 최종 커밋**

```bash
git add index.html
git commit -m "feat: complete portfolio website - final polish"
```
