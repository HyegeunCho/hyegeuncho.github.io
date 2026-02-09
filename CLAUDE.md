# CLAUDE.md - Project Instructions

## Project Overview
Jekyll 기반 GitHub Pages 블로그. `_familyworship/` 컬렉션에 주간 가정 예배 HTML 문서를 게시합니다.

## Family Worship HTML Style Guide

`_familyworship/2026-02-01.html`을 기준 스타일로 사용합니다. 새로운 HTML 문서를 작성하거나 기존 문서를 수정할 때 아래 가이드를 따릅니다.

### Front Matter
```yaml
---
layout: familyworship
title: "2026년 X월 X일 ~ X일 가정 예배"
date: 2026-XX-XX
description: "목사님 설교 말씀 내용을 바탕으로 아이 눈높이에 맞춰 월요일부터 토요일까지 매일 15분 분량의 가정 예배 계획"
---
```

### External Dependencies
- Tailwind CSS: `https://cdn.tailwindcss.com`
- Google Fonts: `Noto Sans KR` (300,400,500,700), `Outfit` (400,600,800), `Nanum Myeongjo` (700)

### Tailwind Config
```js
tailwind.config = {
    theme: {
        extend: {
            colors: {
                brand: { 50: '#f0f9ff', 100: '#e0f2fe', 200: '#bae6fd', 500: '#0ea5e9', 600: '#0284c7', 700: '#0369a1' },
                pastel: { blue: '#e0f2fe', green: '#f0fdf4', yellow: '#fefce8', purple: '#f5f3ff', rose: '#fff1f2', orange: '#fff7ed' }
            },
            fontFamily: {
                sans: ['Noto Sans KR', 'sans-serif'],
                display: ['Outfit', 'Noto Sans KR', 'sans-serif'],
                serif: ['Nanum Myeongjo', 'serif'],
            },
            animation: {
                'fade-in-up': 'fadeInUp 0.8s ease-out forwards',
                'float': 'float 6s ease-in-out infinite',
            },
            keyframes: {
                fadeInUp: { '0%': { opacity: '0', transform: 'translateY(20px)' }, '100%': { opacity: '1', transform: 'translateY(0)' } },
                float: { '0%, 100%': { transform: 'translateY(0)' }, '50%': { transform: 'translateY(-10px)' } }
            }
        }
    }
}
```

### Custom CSS
```css
body {
    background-color: #f8fafc;
    background-image:
        radial-gradient(at 0% 0%, hsla(202,100%,90%,1) 0, transparent 50%),
        radial-gradient(at 50% 0%, hsla(142,100%,95%,1) 0, transparent 50%),
        radial-gradient(at 100% 0%, hsla(30,100%,95%,1) 0, transparent 50%);
    background-attachment: fixed;
}
.glass-card {
    background: rgba(255, 255, 255, 0.7);
    backdrop-filter: blur(12px);
    border: 1px solid rgba(255, 255, 255, 0.4);
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
.glass-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.05), 0 8px 10px -6px rgb(0 0 0 / 0.05);
    background: rgba(255, 255, 255, 0.85);
}
.day-badge {
    font-family: 'Outfit', sans-serif;
    letter-spacing: -0.02em;
}
```

### Body
```html
<body class="antialiased text-slate-800 font-sans pb-20">
```

### Page Layout Structure

#### Header
```html
<header class="relative pt-20 pb-12 px-6 overflow-hidden">
    <div class="max-w-4xl mx-auto text-center relative z-10 animate-fade-in-up">
        <span class="inline-block py-1 px-4 rounded-full bg-brand-100 text-brand-700 text-sm font-bold mb-4 tracking-wider uppercase">Family Worship Plan</span>
        <h1 class="text-4xl md:text-6xl font-black font-display text-slate-900 mb-6 leading-tight">
            {주제 제목} <br>
            <span class="text-transparent bg-clip-text bg-gradient-to-r from-brand-600 to-indigo-600">{부제}</span>
        </h1>
        <div class="max-w-2xl mx-auto">
            <p class="text-lg md:text-xl text-slate-600 leading-relaxed font-light">{설명 문구}</p>
        </div>
    </div>
    <!-- Animated Background Elements -->
    <div class="absolute top-10 left-10 w-32 h-32 bg-blue-200 rounded-full mix-blend-multiply filter blur-2xl opacity-30 animate-float"></div>
    <div class="absolute top-20 right-10 w-40 h-40 bg-purple-200 rounded-full mix-blend-multiply filter blur-2xl opacity-30 animate-float" style="animation-delay: 2s"></div>
</header>
```

#### Main Grid
- 컨테이너: `<main class="max-w-6xl mx-auto px-6">`
- 그리드: `grid grid-cols-1 md:grid-cols-2 gap-8` (2열 레이아웃)

### Day Card (article) Structure

각 요일은 `<article>` 태그를 사용합니다. 구조는 다음과 같습니다:

```html
<article class="glass-card rounded-[2.5rem] p-8 md:p-10 flex flex-col h-full animate-fade-in-up" style="animation-delay: {0.1s ~ 0.6s}">
    <!-- 1. Day Badge: 번호 + 요일 -->
    <div class="flex items-center justify-between mb-6">
        <span class="day-badge text-4xl font-black text-{color}-200">{01~06}</span>
        <span class="px-4 py-1 rounded-full bg-{color}-50 text-{color}-600 font-bold text-sm">{요일}</span>
    </div>

    <!-- 2. Title -->
    <h2 class="text-2xl font-bold mb-4 text-slate-900">{제목}</h2>

    <!-- 3. Content Description -->
    <div class="p-4 bg-white/50 rounded-2xl mb-6 border border-white/40">
        <p class="text-slate-700 leading-relaxed">{본문 설명}</p>
    </div>

    <!-- 4. Bible Verse -->
    <div class="mb-6">
        <h3 class="flex items-center text-sm font-bold text-slate-400 uppercase tracking-widest mb-3">
            <span class="w-2 h-2 bg-{color}-400 rounded-full mr-2"></span> Bible Verse
        </h3>
        <p class="font-serif italic text-lg text-slate-700 pl-4 border-l-2 border-{color}-200">{성경 구절}</p>
    </div>

    <!-- 5. Sharing + Prayer (flex-grow container) -->
    <div class="space-y-6 flex-grow">
        <!-- 나눔 (Sharing) -->
        <section>
            <h4 class="text-sm font-bold text-{color}-600 mb-2">나눔 (Sharing)</h4>
            <ul class="space-y-2">
                <li class="flex items-start"><span class="text-{color}-400 mr-2">•</span> <span class="text-sm text-slate-600">{질문}</span></li>
                <!-- 질문 3개 -->
            </ul>
        </section>

        <!-- 기도문 -->
        <section class="p-5 bg-{color}-50/50 rounded-2xl">
            <h4 class="text-xs font-bold text-{color}-500 uppercase tracking-tighter mb-2">간단한 기도문</h4>
            <p class="text-slate-700 text-[15px] font-medium leading-relaxed">"{기도문}"</p>
        </section>
    </div>

    <!-- 6. Footer: Application + Challenge -->
    <div class="mt-8 pt-6 border-t border-slate-100 grid grid-cols-2 gap-4">
        <div>
            <span class="text-[10px] font-black text-slate-400 uppercase block mb-1">Application</span>
            <p class="text-xs text-slate-500">{적용}</p>
        </div>
        <div>
            <span class="text-[10px] font-black text-slate-400 uppercase block mb-1">Challenge</span>
            <p class="text-xs text-slate-500">{도전}</p>
        </div>
    </div>
</article>
```

### Day Color Scheme (요일별 색상)

| Day | 요일 | Color Token |
|-----|------|-------------|
| 01  | 월요일 | `blue`    |
| 02  | 화요일 | `green`   |
| 03  | 수요일 | `amber`   |
| 04  | 목요일 | `rose`    |
| 05  | 금요일 | `indigo`  |
| 06  | 토요일 | `violet`  |

### JavaScript (Scroll Animation)
```js
const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add('animate-fade-in-up');
            observer.unobserve(entry.target);
        }
    });
}, { threshold: 0.1 });
document.querySelectorAll('article').forEach(card => observer.observe(card));
```

### Key Rules
- 각 day card에 `animation-delay`를 0.1s씩 증가 (0.1s ~ 0.6s)
- 카드 태그는 `<article>` 사용 (`<section>` 아님)
- 그리드는 2열 (`md:grid-cols-2`), 3열 사용하지 않음
- 카드 내부에 이모지 아이콘 사용하지 않음
- 별도의 floating 버튼(scroll-to-top 등) 추가하지 않음
- `main` 패딩은 `px-6`, `pb-20`은 body에 적용
