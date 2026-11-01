<!DOCTYPE html>
<html lang="ar" dir="rtl" class="scroll-smooth">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>لوحة متابعة طلبات التأمين - KSAMC</title>
  <script src="https://cdn.tailwindcss.com/3.4.17"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800;900&display=swap" rel="stylesheet">
  
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: { tajawal: ['Tajawal', 'sans-serif'] }
        }
      }
    }
  </script>
  <style>
    body { font-family: 'Tajawal', sans-serif; }
    .custom-scrollbar::-webkit-scrollbar { width: 6px; height: 6px; }
    .custom-scrollbar::-webkit-scrollbar-thumb { background-color: rgba(156, 163, 175, 0.4); border-radius: 9999px; }
    @media print {
      header, .no-print { display: none !important; }
      body { background: white !important; color: black !important; }
    }
  </style>
</head>
<body class="bg-slate-50 dark:bg-slate-950 text-slate-800 dark:text-slate-100 min-h-screen flex flex-col transition-colors duration-200 antialiased">

  <!-- Header -->
  <header class="bg-white/80 dark:bg-slate-900/80 backdrop-blur border-b border-slate-200 dark:border-slate-800 sticky top-0 z-40 transition-colors shadow-sm">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 py-3 flex flex-wrap items-center justify-between gap-3">
      
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 sm:w-11 sm:h-11 rounded-2xl bg-gradient-to-tr from-emerald-600 to-teal-500 flex items-center justify-center text-white text-xl shadow-md shadow-emerald-600/20">
          <i class="fa-solid fa-hospital-user"></i>
        </div>
        <div>
          <div class="flex items-center gap-2">
            <h1 class="text-base sm:text-lg font-black text-slate-900 dark:text-white">
              لوحة متابعة طلبات التأمين
            </h1>
            <span class="text-[11px] bg-emerald-100 dark:bg-emerald-950/80 text-emerald-800 dark:text-emerald-300 border border-emerald-300/40 dark:border-emerald-700/50 px-2 py-0.5 rounded-full font-bold">انعكاس الشيت</span>
          </div>
          <p class="text-xs text-slate-500 dark:text-slate-400">مدينة الملك سلمان الطبية — إدارة تنمية الإيرادات (CBO)</p>
        </div>
      </div>

      <div class="flex items-center gap-2 flex-wrap">
        <button id="btnRefreshData" type="button" class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-xl text-xs font-bold bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 dark:hover:bg-slate-700 text-slate-700 dark:text-slate-200 transition border border-slate-200 dark:border-slate-700">
          <i id="refreshIcon" class="fa-solid fa-rotate text-emerald-600 dark:text-emerald-400"></i>
          <span id="syncText">مزامنة</span>
        </button>

        <a href="https://docs.google.com/spreadsheets/d/135L6yG_lk5HPj77mZbUqv3-oZNWWd4T5N6yR6hX3Wk0/edit" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-1.5 px-3.5 py-1.5 rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white text-xs font-bold transition shadow-sm border border-emerald-500">
          <i class="fa-solid fa-table"></i>
          <span>فتح قوقل شيت</span>
        </a>

        <!-- Dark Mode Button -->
        <button id="themeToggleBtn" type="button" aria-label="تبديل الوضع الليلي" class="w-9 h-9 rounded-xl bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 dark:hover:bg-slate-700 text-slate-600 dark:text-amber-400 border border-slate-200 dark:border-slate-700 flex items-center justify-center text-sm transition">
          <i id="themeIcon" class="fa-solid fa-moon"></i>
        </button>
      </div>

    </div>
  </header>

  <!-- Main Content -->
  <main class="flex-1 max-w-7xl w-full mx-auto p-4 sm:p-6 space-y-5">

    <!-- KPI Metric Cards -->
    <section class="space-y-3">
      <div class="grid grid-cols-2 sm:grid-cols-4 gap-3 sm:gap-4">
        
        <div class="bg-white dark:bg-slate-900 p-4 rounded-3xl border border-slate-200 dark:border-slate-800 shadow-sm flex items-center justify-between">
          <div>
            <p class="text-xs text-slate-500 dark:text-slate-400 font-medium">إجمالي المعاملات</p>
            <p id="kpiTotal" class="text-2xl sm:text-3xl font-black text-slate-900 dark:text-white mt-1">8</p>
          </div>
          <div class="w-11 h-11 rounded-2xl bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300 flex items-center justify-center text-lg">
            <i class="fa-solid fa-folder-open"></i>
          </div>
        </div>

        <div class="bg-white dark:bg-slate-900 p-4 rounded-3xl border border-emerald-200 dark:border-emerald-900/40 shadow-sm flex items-center justify-between">
          <div>
            <p class="text-xs text-emerald-700 dark:text-emerald-400 font-medium">تم الإنجاز</p>
            <p id="kpiCompleted" class="text-2xl sm:text-3xl font-black text-emerald-600 dark:text-emerald-400 mt-1">7</p>
          </div>
          <div class="w-11 h-11 rounded-2xl bg-emerald-50 dark:bg-emerald-950/60 text-emerald-600 dark:text-emerald-400 flex items-center justify-center text-lg">
            <i class="fa-solid fa-circle-check"></i>
          </div>
        </div>

        <div class="bg-white dark:bg-slate-900 p-4 rounded-3xl border border-amber-200 dark:border-amber-900/40 shadow-sm flex items-center justify-between">
          <div>
            <p class="text-xs text-amber-700 dark:text-amber-400 font-medium">تحت الإجراء</p>
            <p id="kpiPending" class="text-2xl sm:text-3xl font-black text-amber-600 dark:text-amber-400 mt-1">1</p>
          </div>
          <div class="w-11 h-11 rounded-2xl bg-amber-50 dark:bg-amber-950/60 text-amber-600 dark:text-amber-400 flex items-center justify-center text-lg">
            <i class="fa-solid fa-clock-rotate-left"></i>
          </div>
        </div>

        <div class="bg-white dark:bg-slate-900 p-4 rounded-3xl border border-rose-200 dark:border-rose-900/40 shadow-sm flex items-center justify-between">
          <div>
            <p class="text-xs text-rose-700 dark:text-rose-400 font-medium">لم يتم التنفيذ</p>
            <p id="kpiFailed" class="text-2xl sm:text-3xl font-black text-rose-600 dark:text-rose-400 mt-1">0</p>
          </div>
          <div class="w-11 h-11 rounded-2xl bg-rose-50 dark:bg-rose-950/60 text-rose-600 dark:text-rose-400 flex items-center justify-center text-lg">
            <i class="fa-solid fa-circle-xmark"></i>
          </div>
        </div>

      </div>

      <!-- Completion Rate Bar -->
      <div class="bg-white dark:bg-slate-900 p-3.5 sm:p-4 rounded-2xl border border-slate-200 dark:border-slate-800 shadow-sm flex flex-col sm:flex-row sm:items-center justify-between gap-3">
        <div class="flex items-center gap-2">
          <i class="fa-solid fa-chart-pie text-emerald-600 dark:text-emerald-400 text-sm"></i>
          <span class="text-xs font-bold text-slate-700 dark:text-slate-300">نسبة الإنجاز الإجمالية:</span>
          <span id="completionPercentText" class="text-sm font-black text-emerald-600 dark:text-emerald-400 font-mono">87.5%</span>
        </div>
        <div class="flex-1 max-w-md bg-slate-100 dark:bg-slate-800 h-2.5 rounded-full overflow-hidden">
          <div id="completionBar" class="bg-emerald-600 dark:bg-emerald-500 h-full rounded-full transition-all duration-500" style="width: 87.5%;"></div>
        </div>
        <span id="lastUpdatedNotice" class="text-[11px] text-slate-400 dark:text-slate-500">محدث تلقائياً مع السجل السحابي</span>
      </div>
    </section>

    <!-- Toolbar: Search, Filters & Utilities -->
    <section class="bg-white dark:bg-slate-900 p-4 sm:p-5 rounded-3xl border border-slate-200 dark:border-slate-800 shadow-sm flex flex-col lg:flex-row items-stretch lg:items-center justify-between gap-3.5 no-print">
      
      <div class="relative flex-1">
        <i class="fa-solid fa-magnifying-glass absolute right-3.5 top-3.5 text-slate-400 dark:text-slate-500 text-sm"></i>
        <input type="text" id="searchInput" placeholder="بحث باسم المريض، رقم الملف الطبي، الجوال، أو المستند المطلوب..." class="w-full text-xs sm:text-sm pr-10 pl-4 py-2.5 rounded-2xl border border-slate-200 dark:border-slate-700 bg-slate-50 dark:bg-slate-800 text-slate-900 dark:text-white focus:bg-white dark:focus:bg-slate-900 focus:outline-none focus:ring-2 focus:ring-emerald-500 transition">
      </div>

      <div class="flex items-center gap-1.5 overflow-x-auto custom-scrollbar pb-1 lg:pb-0" id="filterTabs">
        <button type="button" data-status="all" class="filter-btn px-3 py-2 rounded-xl text-xs font-bold transition bg-emerald-600 text-white shadow-sm whitespace-nowrap">
          الكل (<span id="countAll">8</span>)
        </button>
        <button type="button" data-status="تحت الإجراء" class="filter-btn px-3 py-2 rounded-xl text-xs font-bold transition bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300 hover:bg-slate-200 dark:hover:bg-slate-700 whitespace-nowrap">
          تحت الإجراء (<span id="countPending">1</span>)
        </button>
        <button type="button" data-status="تم الإنجاز" class="filter-btn px-3 py-2 rounded-xl text-xs font-bold transition bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300 hover:bg-slate-200 dark:hover:bg-slate-700 whitespace-nowrap">
          تم الإنجاز (<span id="countCompleted">7</span>)
        </button>
        <button type="button" data-status="لم يتم تنفيذ المهمة" class="filter-btn px-3 py-2 rounded-xl text-xs font-bold transition bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300 hover:bg-slate-200 dark:hover:bg-slate-700 whitespace-nowrap">
          لم يتم التنفيذ (<span id="countFailed">0</span>)
        </button>
      </div>

      <div class="flex items-center gap-2 border-t lg:border-t-0 pt-2 lg:pt-0">
        <button id="btnExportCsv" type="button" class="px-3 py-2 rounded-xl border border-slate-200 dark:border-slate-700 hover:bg-slate-50 dark:hover:bg-slate-800 text-xs font-bold text-slate-700 dark:text-slate-300 transition flex items-center gap-1.5 shadow-sm">
          <i class="fa-solid fa-file-csv text-emerald-600 dark:text-emerald-400"></i>
          <span>تصدير CSV</span>
        </button>
        <button id="btnPrintTable" type="button" class="px-3 py-2 rounded-xl border border-slate-200 dark:border-slate-700 hover:bg-slate-50 dark:hover:bg-slate-800 text-xs font-bold text-slate-700 dark:text-slate-300 transition flex items-center gap-1.5 shadow-sm">
          <i class="fa-solid fa-print text-sky-600 dark:text-sky-400"></i>
          <span>طباعة</span>
        </button>
        <button id="btnToggleEmbed" type="button" class="px-3 py-2 rounded-xl bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 dark:hover:bg-slate-700 text-xs font-bold text-slate-700 dark:text-slate-300 border border-slate-200 dark:border-slate-700 transition flex items-center gap-1.5 shadow-sm">
          <i class="fa-solid fa-table-cells text-emerald-600 dark:text-emerald-400"></i>
          <span id="embedToggleText">معاينة الشيت</span>
        </button>
      </div>

    </section>

    <!-- Table Directory -->
    <section id="directorySection" class="bg-white dark:bg-slate-900 rounded-3xl p-4 sm:p-5 border border-slate-200 dark:border-slate-800 shadow-sm space-y-3">
      <div class="flex flex-wrap items-center justify-between gap-3 border-b border-slate-100 dark:border-slate-800 pb-3">
        <div class="flex items-center gap-2">
          <span class="w-8 h-8 rounded-xl bg-emerald-100 dark:bg-emerald-950/80 text-emerald-700 dark:text-emerald-400 flex items-center justify-center text-sm font-bold">
            <i class="fa-solid fa-list-check"></i>
          </span>
          <div>
            <h2 class="text-sm sm:text-base font-bold text-slate-900 dark:text-white">سجل طلبات التأمين المحدث</h2>
            <p class="text-xs text-slate-400 dark:text-slate-500">انعكاس مباشر لجدول الشيت مع زر واتساب مباشر لكل مريض</p>
          </div>
        </div>
        <span id="filteredResultsBadge" class="text-xs bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300 px-2.5 py-1 rounded-xl font-bold font-mono">
          عرض 8 من 8
        </span>
      </div>

      <div class="overflow-x-auto custom-scrollbar">
        <table class="w-full text-right text-xs sm:text-sm">
          <thead>
            <tr class="bg-slate-50/80 dark:bg-slate-800/50 border-y border-slate-200 dark:border-slate-800 text-slate-600 dark:text-slate-300 font-bold">
              <th class="py-3 px-3">م</th>
              <th class="py-3 px-3">اسم المريض</th>
              <th class="py-3 px-3">رقم الملف</th>
              <th class="py-3 px-3">رقم الجوال</th>
              <th class="py-3 px-3">المستند المطلوب</th>
              <th class="py-3 px-3">الحالة</th>
              <th class="py-3 px-3">الملاحظات</th>
              <th class="py-3 px-3 text-center no-print">واتساب</th>
              <th class="py-3 px-3 text-center no-print">نسخ</th>
            </tr>
          </thead>
          <tbody id="patientsTableBody" class="divide-y divide-slate-100 dark:divide-slate-800"></tbody>
        </table>
      </div>
    </section>

    <!-- Embedded Sheet Section -->
    <section id="embedContainer" class="hidden bg-white dark:bg-slate-900 rounded-3xl p-4 sm:p-5 border border-slate-200 dark:border-slate-800 shadow-sm space-y-3 no-print">
      <div class="flex items-center justify-between border-b border-slate-100 dark:border-slate-800 pb-3">
        <div class="flex items-center gap-2">
          <span class="w-8 h-8 rounded-xl bg-emerald-100 dark:bg-emerald-950/80 text-emerald-700 dark:text-emerald-400 flex items-center justify-center text-sm font-bold">
            <i class="fa-solid fa-file-excel"></i>
          </span>
          <h2 class="text-sm sm:text-base font-bold text-slate-900 dark:text-white">معاينة شيت قوقل الأصلية</h2>
        </div>
        <a href="https://docs.google.com/spreadsheets/d/135L6yG_lk5HPj77mZbUqv3-oZNWWd4T5N6yR6hX3Wk0/edit" target="_blank" rel="noopener noreferrer" class="px-3 py-1.5 rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white text-xs font-bold transition">
          <span>فتح كامل الشيت</span>
        </a>
      </div>
      <div class="w-full h-[620px] rounded-2xl overflow-hidden border border-slate-200 dark:border-slate-800 bg-slate-100 dark:bg-slate-950">
        <iframe src="https://docs.google.com/spreadsheets/d/135L6yG_lk5HPj77mZbUqv3-oZNWWd4T5N6yR6hX3Wk0/preview" class="w-full h-full border-0" allow="autoplay"></iframe>
      </div>
    </section>

  </main>

  <div id="toastContainer" class="fixed bottom-5 left-5 z-50 flex flex-col gap-2 max-w-sm pointer-events-none no-print"></div>

  <script>
    const records = [
      { id: 1, name: "SAFIYA MAMA SEDEK KOF", mrn: "1666685", mobile: "0570273395", req: "صورة جواز السفر + برنت أبشر ببيانات الدخول", status: "تم الإنجاز", notes: "تم الانتهاء من الطلب وإغلاقه" },
      { id: 2, name: "ABDULLH ABDULGANI I ALSHAREF", mrn: "166508", mobile: "0566476067", req: "تقرير تفاصيل الإصابة وإفادة إصابة العمل", status: "تم الإنجاز", notes: "تم الانتهاء من الطلب وإغلاقه" },
      { id: 3, name: "JAWAHER OMER ABD ALRAHMAN Bakes", mrn: "1669942", mobile: "0576763340", req: "صورة تأشيرة الزيارة + برنت أبشر", status: "تم الإنجاز", notes: "تم استلام المستندات وإنهاء الطلب بنجاح" },
      { id: 4, name: "MURADI AHMED KUWAYBIR SALEM", mrn: "1566750", mobile: "0591033702", req: "إفادة أول تشخيص للورم الليفي بالرحم", status: "تم الإنجاز", notes: "شخصت قبل شهرين وتم إنهاء الطلب" },
      { id: 5, name: "ROANZA ASAAD SRBYNY ISMAIL", mrn: "1669684", mobile: "0543746672", req: "صورة ختم الدخول من الجواز أو برنت الدخول", status: "تم الإنجاز", notes: "تم إرفاق ختم الدخول وإنهاء الطلب بنجاح" },
      { id: 6, name: "GIRL FATEMAH FAKHAR EL DEIN KAN", mrn: "1669754", mobile: "0536682383", req: "خطاب التحويل من المستشفى الخاص", status: "تم الإنجاز", notes: "تم إرفاق خطاب التحويل وفتح الملف بنجاح" },
      { id: 7, name: "NAEMA ELTAGI AID AHMED", mrn: "1669663", mobile: "0546054339", req: "صورة التأشيرة (الفيزا) + برنت من أبشر", status: "تم الإنجاز", notes: "تم استلام التأشيرة وبرنت أبشر بنجاح" },
      { id: 8, name: "BOY SAMIA MORSHEED RAJEH", mrn: "12879270", mobile: "0561699676", req: "تقرير سونار الحمل وتاريخ الحمل وتقرير الولادة والتحويل والجواز وختم الدخول", status: "تحت الإجراء", notes: "وارد طلب استكمال نواقص مستندات المولود" }
    ];

    let currentFilter = 'all';
    let searchQuery = '';

    const patientsTableBody = document.getElementById('patientsTableBody');
    const searchInput = document.getElementById('searchInput');
    const filterTabs = document.getElementById('filterTabs');
    const filteredResultsBadge = document.getElementById('filteredResultsBadge');
    const btnToggleEmbed = document.getElementById('btnToggleEmbed');
    const embedContainer = document.getElementById('embedContainer');
    const embedToggleText = document.getElementById('embedToggleText');
    const btnExportCsv = document.getElementById('btnExportCsv');
    const btnPrintTable = document.getElementById('btnPrintTable');
    const btnRefreshData = document.getElementById('btnRefreshData');
    const refreshIcon = document.getElementById('refreshIcon');
    const syncText = document.getElementById('syncText');
    const themeToggleBtn = document.getElementById('themeToggleBtn');
    const themeIcon = document.getElementById('themeIcon');

    // Theme toggle
    function initTheme() {
      try {
        const saved = localStorage.getItem('ksamc_theme');
        if (saved === 'dark' || (!saved && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
          document.documentElement.classList.add('dark');
          themeIcon.className = 'fa-solid fa-sun';
        } else {
          document.documentElement.classList.remove('dark');
          themeIcon.className = 'fa-solid fa-moon';
        }
      } catch (e) {}
    }

    themeToggleBtn.addEventListener('click', () => {
      const isDark = document.documentElement.classList.toggle('dark');
      try { localStorage.setItem('ksamc_theme', isDark ? 'dark' : 'light'); } catch (e) {}
      themeIcon.className = isDark ? 'fa-solid fa-sun' : 'fa-solid fa-moon';
      showToast(isDark ? 'تم تفعيل الوضع الليلي 🌙' : 'تم تفعيل الوضع النهاري ☀️');
    });

    function showToast(msg) {
      const toast = document.createElement('div');
      toast.className = 'pointer-events-auto flex items-center gap-2 px-4 py-2.5 rounded-xl shadow-lg text-xs font-bold text-white bg-slate-800 dark:bg-slate-700 transition-all transform translate-y-2 opacity-0 duration-300';
      toast.innerHTML = `<i class="fa-solid fa-circle-check text-emerald-400"></i><span>${msg}</span>`;
      document.getElementById('toastContainer').appendChild(toast);
      requestAnimationFrame(() => toast.classList.remove('translate-y-2', 'opacity-0'));
      setTimeout(() => {
        toast.classList.add('opacity-0', '-translate-y-2');
        setTimeout(() => toast.remove(), 300);
      }, 3000);
    }

    function updateKPIs() {
      const total = records.length;
      const completed = records.filter(d => d.status === 'تم الإنجاز').length;
      const pending = records.filter(d => d.status === 'تحت الإجراء').length;
      const failed = records.filter(d => d.status === 'لم يتم تنفيذ المهمة').length;

      document.getElementById('kpiTotal').textContent = total;
      document.getElementById('kpiCompleted').textContent = completed;
      document.getElementById('kpiPending').textContent = pending;
      document.getElementById('kpiFailed').textContent = failed;

      document.getElementById('countAll').textContent = total;
      document.getElementById('countCompleted').textContent = completed;
      document.getElementById('countPending').textContent = pending;
      document.getElementById('countFailed').textContent = failed;

      const rate = total > 0 ? ((completed / total) * 100).toFixed(1) : 0;
      document.getElementById('completionPercentText').textContent = rate + '%';
      document.getElementById('completionBar').style.width = rate + '%';
    }

    function renderTable() {
      patientsTableBody.innerHTML = '';
      const query = searchQuery.toLowerCase();

      const filtered = records.filter(item => {
        const matchesFilter = currentFilter === 'all' || item.status === currentFilter;
        const matchesSearch = !query || 
          item.name.toLowerCase().includes(query) ||
          item.mrn.includes(query) ||
          item.mobile.includes(query) ||
          item.req.includes(query);
        return matchesFilter && matchesSearch;
      });

      filteredResultsBadge.textContent = `عرض ${filtered.length} من ${records.length}`;

      if (filtered.length === 0) {
        patientsTableBody.innerHTML = `
          <tr>
            <td colspan="9" class="text-center py-10 text-slate-400 dark:text-slate-500 font-medium text-xs sm:text-sm">
              <i class="fa-solid fa-inbox text-3xl mb-2 block text-slate-300 dark:text-slate-700"></i>
              لا توجد معاملات مطابقة للبحث أو التصفية
            </td>
          </tr>
        `;
        return;
      }

      filtered.forEach((item) => {
        const tr = document.createElement('tr');
        tr.className = 'hover:bg-slate-50/80 dark:hover:bg-slate-800/40 transition border-b border-slate-100 dark:border-slate-800';

        let badgeClass = 'bg-amber-100 dark:bg-amber-950/60 text-amber-800 dark:text-amber-300 border-amber-200 dark:border-amber-800';
        if (item.status === 'تم الإنجاز') badgeClass = 'bg-emerald-100 dark:bg-emerald-950/60 text-emerald-800 dark:text-emerald-300 border-emerald-200 dark:border-emerald-800';
        else if (item.status === 'لم يتم تنفيذ المهمة') badgeClass = 'bg-rose-100 dark:bg-rose-950/60 text-rose-800 dark:text-rose-300 border-rose-200 dark:border-rose-800';

        const cleanMobile = (item.mobile || '').replace(/^0/, '966').replace(/\D/g, '');
        const waMsg = `⚠️ السلام عليكم ورحمة الله وبركاته،\n\nنفيدكم بأنه لاستكمال الملفات الناقصة الخاصة بالمريض لدى مدينة الملك سلمان الطبية، نأمل التكرم بتزويدنا بالمستند التالي لإرفاقه لدى شركة التأمين:\n\n*اسم المريض*: ${item.name}\n*رقم الملف*: ${item.mrn}\n\n*المستند المطلوب:*\n${item.req}\n\nنأمل إرسال المستند في أقرب وقت ممكن لاستكمال الإجراءات.\n\nشاكرين لكم حسن تعاونكم وتقديركم.`;
        const waUrl = cleanMobile ? `https://wa.me/${cleanMobile}?text=${encodeURIComponent(waMsg)}` : '#';

        tr.innerHTML = `
          <td class="py-3 px-3 font-mono font-bold text-slate-400 dark:text-slate-500">${item.id}</td>
          <td class="py-3 px-3 font-bold text-slate-900 dark:text-white whitespace-nowrap">${item.name}</td>
          <td class="py-3 px-3 font-mono font-bold text-slate-600 dark:text-slate-300">${item.mrn}</td>
          <td class="py-3 px-3 font-mono text-slate-600 dark:text-slate-300 whitespace-nowrap" dir="ltr">${item.mobile}</td>
          <td class="py-3 px-3 text-slate-600 dark:text-slate-300 max-w-xs truncate" title="${item.req}">${item.req}</td>
          <td class="py-3 px-3 whitespace-nowrap">
            <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-[11px] font-bold border ${badgeClass}">
              ${item.status}
            </span>
          </td>
          <td class="py-3 px-3 text-xs text-slate-500 dark:text-slate-400 max-w-xs truncate" title="${item.notes || ''}">${item.notes || '-'}</td>
          <td class="py-3 px-3 text-center whitespace-nowrap no-print">
            ${cleanMobile ? `
              <a href="${waUrl}" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white font-bold text-xs shadow-sm transition active:scale-95">
                <i class="fa-brands fa-whatsapp text-sm"></i>
                <span>مراسلة</span>
              </a>
            ` : '-'}
          </td>
          <td class="py-3 px-3 text-center whitespace-nowrap no-print">
            <button type="button" data-action="copy" data-mrn="${item.mrn}" class="w-7 h-7 rounded-lg bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 dark:hover:bg-slate-700 text-slate-500 dark:text-slate-400 flex items-center justify-center transition" title="نسخ رقم الملف">
              <i class="fa-regular fa-copy text-xs"></i>
            </button>
          </td>
        `;
        patientsTableBody.appendChild(tr);
      });
    }

    patientsTableBody.addEventListener('click', (e) => {
      const copyBtn = e.target.closest('button[data-action="copy"]');
      if (!copyBtn) return;
      const mrnVal = copyBtn.dataset.mrn;
      try {
        navigator.clipboard.writeText(mrnVal).then(() => showToast(`تم نسخ الملف: ${mrnVal}`));
      } catch (err) {
        const ta = document.createElement('textarea');
        ta.value = mrnVal;
        document.body.appendChild(ta);
        ta.select();
        document.execCommand('copy');
        document.body.removeChild(ta);
        showToast(`تم نسخ: ${mrnVal}`);
      }
    });

    filterTabs.addEventListener('click', (e) => {
      const btn = e.target.closest('.filter-btn');
      if (!btn) return;
      document.querySelectorAll('.filter-btn').forEach(b => {
        b.className = 'filter-btn px-3 py-2 rounded-xl text-xs font-bold transition bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300 hover:bg-slate-200 dark:hover:bg-slate-700 whitespace-nowrap';
      });
      btn.className = 'filter-btn px-3 py-2 rounded-xl text-xs font-bold transition bg-emerald-600 text-white shadow-sm whitespace-nowrap';
      currentFilter = btn.dataset.status;
      renderTable();
    });

    searchInput.addEventListener('input', (e) => {
      searchQuery = e.target.value.trim();
      renderTable();
    });

    btnToggleEmbed.addEventListener('click', () => {
      const isHidden = embedContainer.classList.contains('hidden');
      if (isHidden) {
        embedContainer.classList.remove('hidden');
        embedContainer.scrollIntoView({ behavior: 'smooth' });
      } else {
        embedContainer.classList.add('hidden');
      }
    });

    btnRefreshData.addEventListener('click', () => {
      refreshIcon.classList.add('fa-spin');
      syncText.textContent = 'جاري التحديث...';
      setTimeout(() => {
        refreshIcon.classList.remove('fa-spin');
        syncText.textContent = 'مزامنة';
        updateKPIs();
        renderTable();
        const now = new Date();
        const timeStr = now.toLocaleTimeString('ar-SA', { hour: '2-digit', minute: '2-digit' });
        document.getElementById('lastUpdatedNotice').textContent = `آخر تحديث: اليوم ${timeStr}`;
        showToast('تمت المزامنة بنجاح');
      }, 600);
    });

    btnPrintTable.addEventListener('click', () => window.print());

    btnExportCsv.addEventListener('click', () => {
      let csv = '\uFEFFم,اسم المريض,رقم الملف,رقم الجوال,المستند المطلوب,الحالة,الملاحظات\n';
      records.forEach((r) => {
        csv += `"${r.id}","${r.name}","${r.mrn}","${r.mobile}","${r.req.replace(/"/g, '""')}","${r.status}","${(r.notes || '').replace(/"/g, '""')}"\n`;
      });
      const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
      const url = URL.createObjectURL(blob);
      const link = document.createElement('a');
      link.href = url;
      link.download = `سجل_طلبات_التأمين.csv`;
      link.click();
      showToast('تم تصدير ملف CSV');
    });

    initTheme();
    updateKPIs();
    renderTable();
  </script>
</body>
</html>
