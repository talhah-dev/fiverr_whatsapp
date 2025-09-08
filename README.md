<!doctype html>
<html lang="en">

<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>WhatsApp UI — aligned, clean close, no shrink</title>

  <!-- Tailwind -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Font Awesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css"
    crossorigin="anonymous" referrerpolicy="no-referrer" />

  <style>
    .chat-wallpaper {
      background:
        radial-gradient(circle at 2px 2px, rgba(0, 0, 0, .05) 2px, transparent 2px) 0 0/30px 30px,
        linear-gradient(180deg, #efeae2 0%, #e5ddd5 100%);
    }

    .wh-header {
      background: #008069;
    }

    .sent {
      background: #DCF8C6;
    }

    .phone {
      box-shadow: 0 24px 60px rgba(0, 0, 0, .25), 0 3px 12px rgba(0, 0, 0, .12);
    }

    .glass {
      background: linear-gradient(180deg, rgba(255, 255, 255, .78), rgba(255, 255, 255, .58));
      backdrop-filter: blur(18px) saturate(120%);
      -webkit-backdrop-filter: blur(18px) saturate(120%);
      border: 1px solid rgba(255, 255, 255, .45);
    }

    .fade {
      transition: opacity .18s ease-out;
    }

    .pop {
      animation: pop .16s ease-out both;
    }

    @keyframes pop {
      from {
        opacity: 0;
        transform: scale(.98)
      }

      to {
        opacity: 1;
        transform: scale(1)
      }
    }
  </style>
</head>

<body class="min-h-screen bg-neutral-200 flex items-center justify-center p-6">
  <section id="phone" class="phone relative w-[392px] h-[780px] bg-white rounded-[32px] overflow-hidden">
    <!-- Header -->
    <header class="wh-header h-14 px-4 flex items-center gap-3 text-white">
      <i class="fa-solid fa-angle-left text-xl opacity-95"></i>
      <div class="w-9 h-9 rounded-full bg-white/20"></div>
      <div class="flex-1">
        <p class="text-[15px] font-semibold leading-4">Aleyna</p>
        <p class="text-xs text-white/80 leading-4">online</p>
      </div>
      <i class="fa-solid fa-video text-lg opacity-95"></i>
      <i class="fa-solid fa-phone text-lg ml-4 opacity-95"></i>
      <i class="fa-solid fa-ellipsis-vertical text-lg ml-4 opacity-95"></i>
    </header>

    <!-- Chat -->
    <div id="chat" class="chat-wallpaper h-[calc(100%-56px)] overflow-y-auto p-3 pb-24 relative">
      <!-- sent -->
      <div class="space-y-2">
        <div class="flex justify-end">
          <div class="max-w-[72%] rounded-2xl rounded-br-md px-3 py-2 text-[13px] sent">On my way 🚗</div>
        </div>
        <div class="flex justify-end">
          <div class="max-w-[72%] rounded-2xl rounded-br-md px-3 py-2 text-[13px] sent">5 mins</div>
        </div>
      </div>

      <!-- received text -->
      <div class="mt-5">
        <div data-bubble
          class="inline-block max-w-[82%] bg-white rounded-2xl rounded-bl-md px-3 py-2 shadow-sm cursor-pointer">
          <p class="text-[14px] text-neutral-800">
            Aleyna ich komm dich jetzt abholen – hab neuen AMG, lass ihn einweihen
          </p>
          <div class="text-[10px] text-neutral-400 mt-1 text-right">16:54</div>
        </div>
      </div>

      <!-- received image -->
      <div class="mt-4">
        <div data-bubble
          class="inline-block max-w-[88%] rounded-2xl rounded-bl-md overflow-hidden shadow-sm bg-white cursor-pointer">
          <img class="block w-full h-[190px] object-cover"
            src="https://images.unsplash.com/photo-1619767886558-efdc259cde1a?q=80&w=1200&auto=format&fit=crop"
            alt="car" />
          <div class="text-[10px] text-neutral-400 px-2 py-1 text-right">16:54</div>
        </div>
      </div>
    </div>

    <!-- Input -->
    <footer class="absolute bottom-0 left-0 right-0 bg-white border-t px-3 py-2 flex items-center gap-2">
      <i class="fa-regular fa-face-smile text-xl text-neutral-600"></i>
      <input class="flex-1 rounded-full bg-neutral-100 px-4 py-2 text-[14px] outline-none"
        placeholder="Nachricht schreiben…" />
      <i class="fa-solid fa-paperclip text-lg text-neutral-600"></i>
      <button class="w-10 h-10 rounded-full text-white grid place-items-center" style="background:#008069;">
        <i class="fa-solid fa-paper-plane"></i>
      </button>
    </footer>

    <!-- ===== Overlay ===== -->
    <div id="overlay" class="absolute inset-0 hidden">
      <div id="dim" class="bg-black/35 backdrop-blur-[2px] opacity-0 fade z-20 absolute inset-0"></div>

      <div id="stage" class="absolute inset-0 pointer-events-none">
        <!-- crisp clone -->
        <div id="ghost" class="opacity-0 fade absolute z-30"></div>

        <!-- emoji bar (LEFT-ALIGNED WITH SHEET) -->
        <div id="reactions"
          class="glass shadow-lg rounded-full px-3 py-1 flex items-center gap-2 opacity-0 fade absolute z-40">
          <span class="text-[18px] select-none">👍</span>
          <span class="text-[18px] select-none">❤️</span>
          <span class="text-[18px] select-none">😂</span>
          <span class="text-[18px] select-none">😮</span>
          <span class="text-[18px] select-none">😢</span>
          <span class="text-[18px] select-none">🙏</span>
          <span class="text-[18px] select-none">🔥</span>
          <button class="ml-1 w-6 h-6 rounded-full bg-white/40 grid place-items-center text-neutral-700">
            <i class="fa-solid fa-plus text-xs"></i>
          </button>
        </div>

        <!-- dropdown -->
        <div id="sheet"
          class="glass rounded-2xl overflow-hidden shadow-2xl border border-white/40 opacity-0 fade absolute z-50">
          <ul class="text-[14px] min-w-[270px]">
            <li class="flex items-center justify-between px-4 py-3 hover:bg-white/45 transition">
              <span>Antworten</span><i class="fa-solid fa-reply"></i></li>
            <li class="flex items-center justify-between px-4 py-3 hover:bg-white/45 transition">
              <span>Weiterleiten</span><i class="fa-solid fa-share"></i></li>
            <li class="flex items-center justify-between px-4 py-3 hover:bg-white/45 transition"><span>Kopieren</span><i
                class="fa-regular fa-copy"></i></li>
            <li class="flex items-center justify-between px-4 py-3 hover:bg-white/45 transition"><span>Mit Stern
                markieren</span><i class="fa-regular fa-star"></i></li>
            <li class="flex items-center justify-between px-4 py-3 hover:bg-white/45 transition"><span>Fixieren</span><i
                class="fa-solid fa-thumbtack"></i></li>
            <li class="flex items-center justify-between px-4 py-3 hover:bg-white/45 transition"><span>Melden</span><i
                class="fa-regular fa-flag"></i></li>
            <li class="flex items-center justify-between px-4 py-3 hover:bg-red-500/10 text-red-600 transition">
              <span>Löschen</span><i class="fa-solid fa-trash"></i></li>
          </ul>
        </div>
      </div>
    </div>
  </section>

  <script>
    const phone = document.getElementById('phone');
    const chat = document.getElementById('chat');
    const overlay = document.getElementById('overlay');
    const dim = document.getElementById('dim');
    const ghost = document.getElementById('ghost');
    const reactions = document.getElementById('reactions');
    const sheet = document.getElementById('sheet');

    let originalBubble = null;
    const clamp = (v, min, max) => Math.max(min, Math.min(max, v));
    const showOverlay = () => {
      overlay.classList.remove('hidden');
      requestAnimationFrame(() => dim.style.opacity = '1');
    };
    const hideOverlay = () => {
      dim.style.opacity = '0';
      ghost.style.opacity = '0';
      reactions.style.opacity = '0';
      sheet.style.opacity = '0';
      // clear the crisp clone so NO stray timestamp remains
      setTimeout(() => {
        overlay.classList.add('hidden');
        ghost.innerHTML = '';
      }, 160);
    };

    function openFor(bubble) {
      originalBubble = bubble;

      const p = phone.getBoundingClientRect();
      const b = bubble.getBoundingClientRect();
      const pad = 8;

      // show overlay for measuring
      showOverlay();

      // 1) Clone FIRST (keep visible), then hide original with opacity (keeps width)
      const clone = bubble.cloneNode(true);
      clone.removeAttribute('data-bubble');
      clone.style.opacity = '1';
      clone.style.visibility = 'visible';
      clone.style.pointerEvents = 'none';

      bubble.style.opacity = '0';            // <- no width shrink
      bubble.style.pointerEvents = 'none';

      // place the crisp clone
      ghost.innerHTML = '';
      ghost.style.left = (b.left - p.left) + 'px';
      ghost.style.top = (b.top - p.top) + 'px';
      ghost.style.width = b.width + 'px';
      ghost.style.height = b.height + 'px';
      ghost.appendChild(clone);
      ghost.classList.add('pop');
      ghost.style.opacity = '1';

      // prepare for size reads
      reactions.style.left = '0px'; reactions.style.top = '0px'; reactions.style.opacity = '0';
      sheet.style.left = '0px'; sheet.style.top = '0px'; sheet.style.opacity = '0';

      requestAnimationFrame(() => {
        const shW = sheet.offsetWidth, shH = sheet.offsetHeight;
        const rxW = reactions.offsetWidth, rxH = reactions.offsetHeight;

        // SHEET position (prefer below; flip above if near bottom)
        const belowY = (b.top - p.top) + b.height + 10;
        const aboveY = (b.top - p.top) - shH - 10;
        const shTop = ((b.bottom + shH + 40) > p.bottom)
          ? clamp(aboveY, pad, p.height - shH - pad)
          : clamp(belowY, pad, p.height - shH - pad);
        const shLeft = clamp(b.left - p.left, pad, p.width - shW - pad);
        sheet.style.left = shLeft + 'px';
        sheet.style.top = shTop + 'px';
        sheet.classList.add('pop');
        sheet.style.opacity = '1';

        // EMOJI bar: align LEFT EDGE with sheet
        let rxLeft = shLeft; // <— requested alignment
        let rxTop = (b.top - p.top) - rxH - 8;
        if (rxTop < pad) rxTop = (b.top - p.top) + b.height + 8;
        // keep inside frame
        rxLeft = clamp(rxLeft, pad, p.width - rxW - pad);
        reactions.style.left = rxLeft + 'px';
        reactions.style.top = rxTop + 'px';
        reactions.classList.add('pop');
        reactions.style.opacity = '1';
      });
    }

    function closeAll() {
      if (originalBubble) {
        originalBubble.style.opacity = '';
        originalBubble.style.pointerEvents = '';
        originalBubble = null;
      }
      hideOverlay();
    }

    // Open on click
    document.querySelectorAll('[data-bubble]').forEach(b => {
      b.addEventListener('click', e => { e.stopPropagation(); openFor(b); });
    });

    // Close on outside/ESC/scroll
    overlay.addEventListener('click', e => { if (e.target === overlay || e.target === dim) closeAll(); });
    document.addEventListener('keydown', e => { if (e.key === 'Escape' && !overlay.classList.contains('hidden')) closeAll(); });
    chat.addEventListener('scroll', () => { if (!overlay.classList.contains('hidden')) closeAll(); });
  </script>
</body>

</html>