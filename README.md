<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Aventuras Lectoras - 3° Grado Primaria</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts para un look infantil y legible -->
  <link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Quicksand:wght@400;600;700&display=swap" rel="stylesheet">
  <!-- FontAwesome para íconos infantiles -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  
  <style>
    body {
      font-family: 'Quicksand', sans-serif;
      background-color: #f0f9ff;
    }
    .font-kids {
      font-family: 'Fredoka One', cursive;
    }
    /* Estilo de la carta del juego */
    .game-card {
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.08);
      border: 4px solid #ffffff;
    }
    /* Transiciones suaves */
    .transition-all-300 {
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    }
    /* Animación de tambaleo para errores */
    @keyframes wobble {
      0%, 100% { transform: translateX(0); }
      25% { transform: translateX(-6px) rotate(-1deg); }
      75% { transform: translateX(6px) rotate(1deg); }
    }
    .wobble {
      animation: wobble 0.3s ease-in-out;
    }
    /* Animación de flotado para la carita/mascota */
    @keyframes float {
      0%, 100% { transform: translateY(0px); }
      50% { transform: translateY(-10px); }
    }
    .float-animation {
      animation: float 4s ease-in-out infinite;
    }
    /* Impresión limpia */
    @media print {
      .no-print { display: none !important; }
      body { background: white; }
    }
  </style>
</head>
<body class="text-slate-800 pb-16">

  <header class="bg-gradient-to-r from-teal-400 via-cyan-500 to-blue-500 text-white shadow-lg no-print">
    <div class="max-w-7xl mx-auto px-4 py-4 flex flex-col md:flex-row justify-between items-center gap-4">
      <div class="flex items-center gap-3">
        <div class="bg-white text-cyan-600 p-2.5 rounded-2xl shadow-inner text-2xl float-animation">
          🚀
        </div>
        <div>
          <h1 class="text-2xl font-kids tracking-wider">Aventuras Lectoras!</h1>
          <p class="text-xs font-semibold opacity-90">Senacyt 2026 • Grupo G6 • 3.er Grado Primaria</p>
        </div>
      </div>
      
      <!-- Selector de Modo de Trabajo -->
      <div class="bg-white/20 p-1.5 rounded-2xl flex gap-1 backdrop-blur-sm">
        <button id="btn-tab-game" onclick="switchTab('game')" class="px-5 py-2 rounded-xl text-sm font-bold transition-all-300 bg-white text-blue-600 shadow-md">
          🎮 ¡Jugar el Simulador!
        </button>
        <button id="btn-tab-ficha" onclick="switchTab('ficha')" class="px-5 py-2 rounded-xl text-sm font-bold transition-all-300 hover:bg-white/10 text-white">
          📝 Ficha de Codiseño
        </button>
      </div>
    </div>
  </header>

  <!-- Contenedor Principal -->
  <main class="max-w-7xl mx-auto px-4 mt-6">

    <!-- ======================= MODO JUEGO (SIMULADOR) ======================= -->
    <section id="section-game" class="transition-all-300 block">
      
      <!-- Contenedor del Juego -->
      <div class="max-w-3xl mx-auto bg-white rounded-3xl game-card overflow-hidden transition-all-300">
        
        <!-- Barra de progreso e información del nivel -->
        <div id="game-header-bar" class="bg-gradient-to-r from-emerald-400 to-teal-500 text-white p-4 flex justify-between items-center px-6">
          <div class="flex items-center gap-2">
            <span id="game-mascot" class="text-2xl">🐢</span>
            <span id="game-level-title" class="font-kids tracking-wide text-lg">Nivel Fácil</span>
          </div>
          <div class="flex items-center gap-3">
            <span class="bg-white/20 px-3 py-1 rounded-full text-xs font-bold" id="game-text-indicator">Texto: El perro y la pelota</span>
            <span class="bg-amber-400 text-slate-900 font-bold px-3 py-1 rounded-full text-xs shadow-sm flex items-center gap-1">
              ⭐ <span id="star-count">0</span>
            </span>
          </div>
        </div>

        <!-- Cuerpo del Juego (Pantallas dinámicas) -->
        <div class="p-6 md:p-8 min-h-[420px] flex flex-col justify-between" id="game-stage-container">
          
          <!-- PANTALLA 1: Selección de Nivel -->
          <div id="stage-setup" class="space-y-6 block">
            <div class="text-center py-4">
              <h2 class="text-2xl font-kids text-slate-700">¡Hola, Aventurero! 👋</h2>
              <p class="text-slate-500 mt-1 text-sm md:text-base">Elige un nivel para comenzar tu misión de lectura y juego de palabras.</p>
            </div>

            <!-- Cartas de Selección de Nivel -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
              <!-- Fácil -->
              <button onclick="selectLevel('easy')" class="group p-5 bg-emerald-50 hover:bg-emerald-100/80 border-2 border-emerald-200 hover:border-emerald-400 rounded-2xl text-left transition-all-300 shadow-sm hover:shadow-md">
                <div class="flex justify-between items-center mb-2">
                  <span class="text-3xl">🐢</span>
                  <span class="bg-emerald-200 text-emerald-800 font-bold text-xs px-2.5 py-1 rounded-full">FÁCIL</span>
                </div>
                <h3 class="font-kids text-lg text-emerald-900">Nivel Tortuga</h3>
                <p class="text-xs text-emerald-700/80 mt-1 font-semibold">60 seg • 5 oraciones sencillas.</p>
              </button>

              <!-- Normal -->
              <button onclick="selectLevel('normal')" class="group p-5 bg-sky-50 hover:bg-sky-100/80 border-2 border-sky-200 hover:border-sky-400 rounded-2xl text-left transition-all-300 shadow-sm hover:shadow-md">
                <div class="flex justify-between items-center mb-2">
                  <span class="text-3xl">🐇</span>
                  <span class="bg-sky-200 text-sky-800 font-bold text-xs px-2.5 py-1 rounded-full">NORMAL</span>
                </div>
                <h3 class="font-kids text-lg text-sky-900">Nivel Conejo</h3>
                <p class="text-xs text-sky-700/80 mt-1 font-semibold">45 seg • Vocabulario divertido.</p>
              </button>

              <!-- Difícil -->
              <button onclick="selectLevel('hard')" class="group p-5 bg-rose-50 hover:bg-rose-100/80 border-2 border-rose-200 hover:border-rose-400 rounded-2xl text-left transition-all-300 shadow-sm hover:shadow-md">
                <div class="flex justify-between items-center mb-2">
                  <span class="text-3xl">🦅</span>
                  <span class="bg-rose-200 text-rose-800 font-bold text-xs px-2.5 py-1 rounded-full">DIFÍCIL</span>
                </div>
                <h3 class="font-kids text-lg text-rose-900">Nivel Águila</h3>
                <p class="text-xs text-rose-700/80 mt-1 font-semibold">30 seg • Textos más largos.</p>
              </button>
            </div>

            <!-- Mascota Instructiva -->
            <div class="bg-amber-50 border-2 border-amber-200 rounded-2xl p-4 flex gap-3 items-start">
              <span class="text-3xl float-animation">🧠</span>
              <div>
                <h4 class="font-bold text-sm text-amber-900">¿Cuál es el secreto?</h4>
                <p class="text-xs text-amber-800 leading-relaxed mt-1">
                  Muchos leen rápido pero no recuerdan lo que leyeron. El secreto es leer con atención, comprender la historia y ¡prepararse para ordenar las letras misteriosas!
                </p>
              </div>
            </div>
          </div>

          <!-- PANTALLA 2: Lectura de Texto -->
          <div id="stage-reading" class="space-y-6 hidden">
            <!-- Barra de cuenta regresiva -->
            <div>
              <div class="flex justify-between items-center text-xs font-bold text-slate-500 mb-1.5">
                <span>⏱️ TIEMPO PARA LEER: <span id="timer-number">60</span>s</span>
                <span class="text-emerald-600">¡Lee con calma y atención!</span>
              </div>
              <div class="w-full h-3.5 bg-slate-100 rounded-full overflow-hidden border border-slate-200">
                <div id="timer-progress-bar" class="h-full bg-gradient-to-r from-teal-400 to-emerald-500 transition-all duration-1000" style="width: 100%"></div>
              </div>
            </div>

            <!-- Texto de lectura principal -->
            <div class="bg-amber-50/50 border-4 border-amber-100 p-6 md:p-8 rounded-3xl shadow-sm relative">
              <span class="absolute -top-3 left-6 bg-amber-400 text-amber-950 px-4 py-0.5 rounded-full text-xs font-bold font-kids">
                ¡Misión Lectora! 📖
              </span>
              <h3 id="reading-title" class="font-kids text-xl text-slate-800 mb-3 text-center">Título del Cuento</h3>
              <p id="reading-body" class="text-base md:text-lg text-slate-700 leading-relaxed text-justify first-letter:text-3xl first-letter:font-kids first-letter:text-teal-600">
                Texto del cuento aquí...
              </p>
            </div>

            <!-- Botón listo antes de tiempo -->
            <div class="flex justify-center">
              <button onclick="finishReadingEarly()" class="bg-gradient-to-r from-emerald-500 to-teal-600 text-white font-kids text-lg px-8 py-3.5 rounded-2xl hover:scale-105 active:scale-95 shadow-md transition-all-300">
                ✨ ¡Ya terminé de leer! ✨
              </button>
            </div>
          </div>

          <!-- PANTALLA 3: Preguntas de Comprensión (1 por 1) -->
          <div id="stage-quiz" class="space-y-6 hidden">
            <div class="flex justify-between items-center bg-slate-50 p-3 rounded-2xl border">
              <span class="text-xs font-bold text-slate-500">PREGUNTA <span id="quiz-index-indicator">1/3</span></span>
              <div class="flex gap-1" id="quiz-dots">
                <span class="w-3 h-3 rounded-full bg-slate-200"></span>
                <span class="w-3 h-3 rounded-full bg-slate-200"></span>
                <span class="w-3 h-3 rounded-full bg-slate-200"></span>
              </div>
            </div>

            <div class="space-y-4">
              <h3 id="quiz-question" class="text-lg md:text-xl font-bold text-slate-800">¿Qué hace el perro Tobi en el jardín?</h3>
              
              <!-- Opciones de Respuesta -->
              <div id="quiz-options-container" class="grid grid-cols-1 gap-3">
                <!-- Se generan dinámicamente -->
              </div>
            </div>

            <!-- Caja de Pistas (Filtro Pedagógico Amigable) -->
            <div id="quiz-hint-box" class="bg-yellow-50 border-2 border-yellow-200 rounded-2xl p-4 hidden">
              <div class="flex gap-2 items-start">
                <span class="text-2xl float-animation">💡</span>
                <div>
                  <h4 class="font-bold text-xs text-yellow-900">Pista del Sabio:</h4>
                  <p id="quiz-hint-text" class="text-xs text-yellow-800 font-semibold mt-0.5 leading-relaxed">¿Recuerdas la primera oración? Qué mascota se menciona...</p>
                </div>
              </div>
            </div>
          </div>

          <!-- PANTALLA 4: ¡Arma Palabras! (Módulo Interactivo) -->
          <div id="stage-wordbuilder" class="space-y-6 hidden">
            <div class="text-center">
              <span class="bg-violet-100 text-violet-700 font-kids text-xs px-4 py-1 rounded-full uppercase tracking-wider">
                🧩 ¡NUEVO RETO DIVERTIDO!
              </span>
              <h3 class="font-kids text-2xl text-violet-800 mt-2">¡Arma la Palabra Secreta!</h3>
              <p class="text-xs text-slate-500 mt-1">Ordena las letras para formar la palabra que apareció en el cuento.</p>
            </div>

            <!-- Pista de la Palabra -->
            <div class="bg-violet-50 border-2 border-violet-100 rounded-2xl p-3 text-center max-w-md mx-auto">
              <p class="text-xs text-slate-500 font-bold uppercase tracking-wider">Pista de la Palabra:</p>
              <p id="wordbuilder-hint" class="text-sm font-semibold text-violet-900 mt-0.5">"El juguete favorito de Tobi que cayó al río"</p>
            </div>

            <!-- Letras vacías de destino (La palabra que se va formando) -->
            <div class="flex flex-wrap justify-center gap-2 py-4" id="wordbuilder-slots">
              <!-- Cajas vacías ej: [P] [E] [L] [ ] [ ] [ ] -->
            </div>

            <!-- Letras mezcladas de origen (Tappables) -->
            <div class="flex flex-wrap justify-center gap-3 py-2 bg-slate-50 p-4 rounded-3xl border border-dashed" id="wordbuilder-pool">
              <!-- Letras mezcladas listas para cliquear -->
            </div>

            <!-- Botones de Control de Armado -->
            <div class="flex justify-center gap-3">
              <button onclick="resetWordBuilder()" class="bg-slate-200 hover:bg-slate-300 text-slate-700 font-bold text-sm px-5 py-2.5 rounded-xl transition-all-300">
                🧹 Reiniciar Letras
              </button>
              <button onclick="checkWordBuilderSolution()" class="bg-gradient-to-r from-violet-500 to-purple-600 text-white font-kids text-base px-8 py-2.5 rounded-xl hover:scale-105 active:scale-95 shadow-md transition-all-300">
                🚀 ¡Revisar Palabra!
              </button>
            </div>
          </div>

          <!-- PANTALLA 5: Reflexión Final -->
          <div id="stage-reflection" class="space-y-6 hidden">
            <div class="text-center">
              <span class="text-4xl">✍️</span>
              <h3 class="font-kids text-2xl text-slate-800 mt-2">¡Casi terminamos, Escritor!</h3>
              <p class="text-xs text-slate-500 mt-1">Escribe una oración explicando con tus propias palabras lo que aprendiste de la historia.</p>
            </div>

            <div class="space-y-2">
              <label class="text-xs font-bold text-slate-600">Tu respuesta libre (Mínimo 15 letras):</label>
              <textarea id="reflection-textarea" oninput="validateReflection()" placeholder="Ejemplo: El cuento trata sobre el perro Tobi que recuperó su pelota roja gracias a su dueño..." class="w-full border-2 border-slate-200 focus:border-cyan-400 focus:bg-white bg-slate-50 rounded-2xl p-4 text-sm font-semibold transition-all-300 min-h-[110px] resize-none"></textarea>
              <div class="flex justify-between items-center text-xs">
                <span id="reflection-char-count" class="text-slate-400 font-semibold">0 / 15 caracteres mínimos</span>
                <span class="text-cyan-600 font-bold">¡Esta es tu verdadera señal de comprensión! 🌟</span>
              </div>
            </div>

            <div class="flex justify-center">
              <button id="btn-submit-reflection" disabled onclick="submitReflection()" class="bg-slate-300 text-slate-500 font-kids text-lg px-10 py-3.5 rounded-2xl cursor-not-allowed transition-all-300">
                🏁 ¡Finalizar Aventura!
              </button>
            </div>
          </div>

          <!-- PANTALLA 6: Reporte de Resultados -->
          <div id="stage-results" class="space-y-6 hidden text-center">
            <div>
              <div id="result-emoji" class="text-6xl float-animation">😄</div>
              <h3 id="result-title" class="font-kids text-2xl text-slate-800 mt-3">¡Excelente Trabajo!</h3>
              <p id="result-subtitle" class="text-slate-500 text-xs md:text-sm">Has demostrado una gran atención al comprender el texto.</p>
            </div>

            <!-- Estadísticas en tarjeta -->
            <div class="bg-slate-50 border-2 rounded-2xl p-4 grid grid-cols-3 gap-2 max-w-md mx-auto">
              <div class="p-2">
                <span class="block text-xl md:text-2xl font-kids text-amber-500" id="stat-stars">0</span>
                <span class="text-[10px] font-bold text-slate-400 uppercase">Estrellas</span>
              </div>
              <div class="p-2 border-x">
                <span class="block text-xl md:text-2xl font-kids text-emerald-500" id="stat-quiz">0/3</span>
                <span class="text-[10px] font-bold text-slate-400 uppercase">Preguntas</span>
              </div>
              <div class="p-2">
                <span class="block text-xl md:text-2xl font-kids text-violet-500" id="stat-word">¡Logrado!</span>
                <span class="text-[10px] font-bold text-slate-400 uppercase">Vocabulario</span>
              </div>
            </div>

            <!-- Resumen de Reflexión Escrita -->
            <div class="bg-amber-50/50 border border-amber-100 rounded-2xl p-3 max-w-md mx-auto text-left">
              <span class="text-[10px] font-bold text-amber-800 uppercase block mb-1">Tu diario de reflexión:</span>
              <p id="result-reflection-text" class="text-xs text-slate-600 italic font-semibold leading-relaxed">"..."</p>
            </div>

            <!-- Botones de Acción final -->
            <div class="flex flex-col sm:flex-row gap-3 justify-center pt-2">
              <button onclick="retryCurrentLevel()" class="bg-amber-400 hover:bg-amber-500 text-slate-900 font-kids text-sm px-6 py-3 rounded-xl transition-all-300 shadow-md">
                🔄 Jugar de Nuevo
              </button>
              <button onclick="resetToSetup()" class="bg-gradient-to-r from-teal-500 to-cyan-600 text-white font-kids text-sm px-6 py-3 rounded-xl transition-all-300 shadow-md">
                🗺️ Elegir Otro Nivel
              </button>
            </div>
          </div>

        </div>
      </div>
    </section>

    <!-- ======================= MODO FICHA PEDAGÓGICA (DOCENTES) ======================= -->
    <section id="section-ficha" class="transition-all-300 hidden no-print max-w-5xl mx-auto space-y-6">
      
      <!-- Panel de Instrucciones Pedagógicas de la IA -->
      <div class="bg-blue-50 border-2 border-blue-200 rounded-2xl p-5 flex flex-col md:flex-row items-center gap-4">
        <div class="bg-blue-500 text-white p-3.5 rounded-full text-2xl shadow-inner">
          👩‍🏫
        </div>
        <div class="text-center md:text-left">
          <h2 class="font-kids text-lg text-blue-950">¡Cerebro Pedagógico Sincronizado!</h2>
          <p class="text-xs text-blue-800 leading-relaxed mt-0.5">
            ¡Modifica la ficha! Todo lo que edites aquí —textos, preguntas, respuestas, pistas e incluso la palabra del minijuego— se cargará inmediatamente al presionar el botón <b>"Sincronizar con el Juego"</b>. ¡Diseño didáctico dinámico en vivo!
          </p>
        </div>
        <div class="flex gap-2 shrink-0">
          <button onclick="syncFichaToGame()" class="bg-emerald-500 hover:bg-emerald-600 text-white font-kids text-sm px-4 py-2.5 rounded-xl shadow-md transition-all-300">
            🔄 Sincronizar
          </button>
          <button onclick="window.print()" class="bg-blue-600 hover:bg-blue-700 text-white font-kids text-sm px-4 py-2.5 rounded-xl shadow-md transition-all-300">
            🖨️ PDF
          </button>
        </div>
      </div>

      <!-- DATOS DEL GRUPO -->
      <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200">
        <div class="bg-slate-800 text-slate-100 px-4 py-2 rounded-xl text-xs font-bold tracking-wide uppercase mb-4 flex items-center gap-2">
          <span>👥</span> Datos del Grupo Investigador
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
          <div>
            <label class="block text-xs font-bold text-slate-500 mb-1">Nombre del Grupo / Ficha</label>
            <input type="text" id="teacher-group-name" value="G6" class="w-full border rounded-lg p-2 text-xs font-semibold bg-slate-50">
          </div>
          <div>
            <label class="block text-xs font-bold text-slate-500 mb-1">Fecha de Sesión</label>
            <input type="date" id="teacher-date" class="w-full border rounded-lg p-2 text-xs font-semibold bg-slate-50">
          </div>
        </div>
        <div class="grid grid-cols-2 md:grid-cols-4 gap-3">
          <div>
            <label class="block text-xs font-bold text-slate-500 mb-1">Docente 1</label>
            <input type="text" placeholder="Nombre completo" class="w-full border rounded-lg p-2 text-xs font-semibold bg-slate-50">
          </div>
          <div>
            <label class="block text-xs font-bold text-slate-500 mb-1">Docente 2</label>
            <input type="text" placeholder="Nombre completo" class="w-full border rounded-lg p-2 text-xs font-semibold bg-slate-50">
          </div>
          <div>
            <label class="block text-xs font-bold text-slate-500 mb-1">Docente 3</label>
            <input type="text" placeholder="Nombre completo" class="w-full border rounded-lg p-2 text-xs font-semibold bg-slate-50">
          </div>
          <div>
            <label class="block text-xs font-bold text-slate-500 mb-1">Docente 4</label>
            <input type="text" placeholder="Nombre completo" class="w-full border rounded-lg p-2 text-xs font-semibold bg-slate-50">
          </div>
        </div>
      </div>

      <!-- PARTE 1: PROBLEMA PEDAGÓGICO REAL -->
      <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200">
        <div class="bg-slate-800 text-slate-100 px-4 py-2 rounded-xl text-xs font-bold tracking-wide uppercase mb-4 flex items-center gap-2">
          <span>📌</span> PARTE 1 — Diagnóstico y Modelo Mental Erróneo
        </div>
        
        <div class="space-y-4">
          <div>
            <label class="block text-xs font-bold text-slate-500 mb-1">1. El error concreto del estudiante</label>
            <textarea class="w-full border rounded-xl p-3 text-xs font-medium leading-relaxed bg-amber-50/50 min-h-[80px]">El estudiante cree que leer en voz alta sin equivocarse equivale a comprender el texto. Lee el párrafo completo pero al terminar no puede decir de qué trató ni identificar la idea principal. Modelo mental incorrecto: "leer = pronunciar las palabras en orden correcto sin entender."</textarea>
          </div>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div>
              <label class="block text-xs font-bold text-slate-500 mb-1">2. Asignatura / Área Curricular</label>
              <input type="text" value="Español / Lengua y Literatura" class="w-full border rounded-xl p-2.5 text-xs font-semibold bg-amber-50/50">
            </div>
            <div>
              <label class="block text-xs font-bold text-slate-500 mb-1">Grado / Nivel Etario</label>
              <input type="text" value="3.er Grado de Primaria (8–9 años)" class="w-full border rounded-xl p-2.5 text-xs font-semibold bg-amber-50/50">
            </div>
          </div>
          <div>
            <label class="block text-xs font-bold text-slate-500 mb-1">3. ¿Por qué una explicación verbal tradicional no es suficiente?</label>
            <textarea class="w-full border rounded-xl p-3 text-xs font-medium leading-relaxed bg-amber-50/50 min-h-[70px]">El estudiante necesita experimentar empíricamente la diferencia entre pronunciar y procesar. Necesita leer un texto divertido y confrontarse de inmediato con el juego interactivo para darse cuenta de si realmente asimiló la información.</textarea>
          </div>
        </div>
      </div>

      <!-- PARTE 2: DISEÑO DEL RECURSO INTERACTIVO -->
      <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200">
        <div class="bg-emerald-800 text-emerald-100 px-4 py-2 rounded-xl text-xs font-bold tracking-wide uppercase mb-4 flex items-center gap-2">
          <span>🛠️</span> PARTE 2 — Diseño Mecánico e Interactivo del Recurso
        </div>

        <div class="space-y-4">
          <div>
            <label class="block text-xs font-bold text-slate-500 mb-1">4. ¿Qué HACE el recurso interactivo? — Parámetros modificados</label>
            <textarea class="w-full border rounded-xl p-3 text-xs font-medium leading-relaxed bg-amber-50/50 min-h-[90px]">• El estudiante elige entre 3 niveles de velocidad de lectura (Fácil 🐢 / Normal 🐇 / Difícil 🦅).
• Cada nivel presenta cuentos aleatorios para desafiar la memoria.
• Un temporizador visual con barra interactiva mide el progreso de lectura activa.
• Un módulo de preguntas aleatorias evalúa la retención con pistas en forma de interrogante.
• NUEVO RETO: Un minijuego de "Armar Palabras" donde se ordenan letras magnéticas para formar vocabulario clave del texto.
• Retroalimentación con caritas emocionales, estrellas y resumen de avances.</textarea>
          </div>
          <div>
            <label class="block text-xs font-bold text-slate-500 mb-1">5. La pista mínima viable (si el estudiante comete un error)</label>
            <textarea class="w-full border rounded-xl p-3 text-xs font-medium leading-relaxed bg-amber-50/50 min-h-[60px]">Una pista en forma de pregunta de andamiaje cognitivo específica que guía la atención del niño a una parte del texto, evitando darle la respuesta correcta de inmediato.</textarea>
          </div>
          <div>
            <label class="block text-xs font-bold text-slate-500 mb-1">6. Señal inequívoca de logro de comprensión</label>
            <textarea class="w-full border rounded-xl p-3 text-xs font-medium leading-relaxed bg-amber-50/50 min-h-[60px]">Responder con éxito la palabra secreta magnética en "Armar Palabras", contestar al menos 2 preguntas de comprensión de forma independiente y escribir una oración coherente en la bitácora final.</textarea>
          </div>
        </div>
      </div>

      <!-- BANCO DE CONTENIDOS EDITABLE Y SINCRONIZADO -->
      <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200">
        <div class="bg-teal-800 text-teal-100 px-4 py-2 rounded-xl text-xs font-bold tracking-wide uppercase mb-2 flex items-center gap-2">
          <span>📚</span> Banco de Cuentos, Preguntas y Palabras del Juego (¡Editable!)
        </div>
        <p class="text-xs text-slate-400 mb-4">Los cambios que realices en estas tarjetas se aplicarán al simulador de juego interactivo.</p>

        <div class="space-y-6" id="editor-texts-container">
          <!-- Se cargan dinámicamente desde el JS para que se puedan editar y sincronizar perfectamente -->
        </div>
      </div>

      <!-- PARTE 3: LISTA DE VERIFICACIÓN PEDAGÓGICA -->
      <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200">
        <div class="bg-amber-600 text-amber-50 px-4 py-2 rounded-xl text-xs font-bold tracking-wide uppercase mb-4 flex items-center gap-2">
          <span>✅</span> PARTE 3 — Autoevaluación del Codiseño
        </div>
        
        <ul class="space-y-2" id="checklist">
          <li onclick="toggleCheckItem(this)" class="flex items-start gap-3 p-3 bg-slate-50 hover:bg-emerald-50 border rounded-xl cursor-pointer transition-all-300">
            <input type="checkbox" checked class="mt-1 accent-emerald-500" onclick="event.stopPropagation(); toggleCheckItem(this.parentElement)">
            <span class="text-xs font-semibold text-slate-700">Describimos el error cognitivo basándonos en el <b>modelo mental</b> del niño, no solo en "no sabe hacer X".</span>
          </li>
          <li onclick="toggleCheckItem(this)" class="flex items-start gap-3 p-3 bg-slate-50 hover:bg-emerald-50 border rounded-xl cursor-pointer transition-all-300">
            <input type="checkbox" checked class="mt-1 accent-emerald-500" onclick="event.stopPropagation(); toggleCheckItem(this.parentElement)">
            <span class="text-xs font-semibold text-slate-700">La pista de error es una <b>pregunta de andamiaje</b> y nunca la respuesta regalada.</span>
          </li>
          <li onclick="toggleCheckItem(this)" class="flex items-start gap-3 p-3 bg-slate-50 hover:bg-emerald-50 border rounded-xl cursor-pointer transition-all-300">
            <input type="checkbox" checked class="mt-1 accent-emerald-500" onclick="event.stopPropagation(); toggleCheckItem(this.parentElement)">
            <span class="text-xs font-semibold text-slate-700">Integramos el minijuego dinámico de <b>"Armar Palabras"</b> para interactuar físicamente con la estructura de la palabra clave.</span>
          </li>
          <li onclick="toggleCheckItem(this)" class="flex items-start gap-3 p-3 bg-slate-50 hover:bg-emerald-50 border rounded-xl cursor-pointer transition-all-300">
            <input type="checkbox" checked class="mt-1 accent-emerald-500" onclick="event.stopPropagation(); toggleCheckItem(this.parentElement)">
            <span class="text-xs font-semibold text-slate-700">El temporizador de lectura es configurable y se adapta a la diversidad de ritmos del salón.</span>
          </li>
        </ul>
        <div id="check-status" class="mt-4 text-xs font-bold text-emerald-600"></div>
      </div>

      <!-- BITÁCORA DE DECISIONES -->
      <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200">
        <div class="bg-violet-800 text-violet-100 px-4 py-2 rounded-xl text-xs font-bold tracking-wide uppercase mb-4 flex items-center gap-2">
          <span>📓</span> Bitácora Docente de Decisiones Vibecoding
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
          <div class="p-4 bg-slate-50 rounded-xl border">
            <h4 class="text-xs font-bold text-violet-900 mb-1">Propuesta original de la IA</h4>
            <textarea class="w-full bg-white border rounded p-2 text-xs min-h-[80px]" placeholder="Ej. El temporizador tradicional de texto estático."></textarea>
          </div>
          <div class="p-4 bg-slate-50 rounded-xl border">
            <h4 class="text-xs font-bold text-violet-900 mb-1">Lo que reestructuramos por interactividad</h4>
            <textarea class="w-full bg-white border rounded p-2 text-xs min-h-[80px]">Decidimos implementar un módulo lúdico de letras móviles llamado 'Armar Palabras', donde los niños manipulan las letras para verificar su memoria ortográfica y comprensión del concepto clave leído.</textarea>
          </div>
          <div class="p-4 bg-slate-50 rounded-xl border">
            <h4 class="text-xs font-bold text-violet-900 mb-1">Valor didáctico observado</h4>
            <textarea class="w-full bg-white border rounded p-2 text-xs min-h-[80px]" placeholder="Ej. El niño no se frustra al equivocarse en las preguntas porque tiene una segunda oportunidad de éxito manipulando las letras de la palabra secreta."></textarea>
          </div>
        </div>
      </div>

    </section>

  </main>

  <script>
    /* BASE DE DATOS INICIAL DE TEXTOS, PREGUNTAS Y MINIJUEGOS "ARMAR PALABRAS" */
    let database = {
      easy: [
        {
          id: "t1",
          level: "easy",
          levelName: "Fácil 🐢",
          title: "El perro y la pelota",
          body: "Tobi es un perro café y muy juguetón. Todos los días sale al patio a buscar su pelota roja. Un día la pelota cayó al río. Tobi miró el agua y esperó. Su dueño fue a buscarla y Tobi movió la cola muy feliz.",
          word: "PELOTA",
          wordHint: "El juguete favorito de Tobi que cayó al agua del río.",
          questions: [
            {
              q: "¿Cómo se llama el perro del cuento?",
              options: ["Tobi", "Coco", "Max", "Pelusa"],
              correctIndex: 0,
              hint: "¿Recuerdas la primera oración? ¿Qué nombre le pusieron al perro?"
            },
            {
              q: "¿Qué le pasó a la pelota de Tobi?",
              options: ["La rompió jugando", "La perdió en la casa", "Cayó al río", "Se la robó un gato"],
              correctIndex: 2,
              hint: "Vuelve a leer la tercera oración. ¿A dónde se fue volando la pelota?"
            },
            {
              q: "¿Cómo se sentía Tobi al final?",
              options: ["Triste y molesto", "Asustado", "Muy feliz", "Cansado"],
              correctIndex: 2,
              hint: "¿Qué hace Tobi con su cola cuando su dueño regresa con su juguete?"
            }
          ]
        },
        {
          id: "t2",
          level: "easy",
          levelName: "Fácil 🐢",
          title: "La nube viajera",
          body: "Había una nube blanca que le gustaba viajar por el cielo. Un día vio un campo seco y triste. La nube se llenó de agua y empezó a llover. Las plantas bebieron el agua y se pusieron verdes. La nube siguió su camino muy contenta.",
          word: "LLUVIA",
          wordHint: "El agua que cae del cielo cuando la nube decide ayudar al campo seco.",
          questions: [
            {
              q: "¿Qué le gustaba hacer a la nube blanca?",
              options: ["Dormir todo el día", "Viajar por el cielo", "Esconder al sol", "Volar bajo el mar"],
              correctIndex: 1,
              hint: "Relee la primera oración. ¿Cuál era el pasatiempo preferido de la nube?"
            },
            {
              q: "¿Qué hizo la nube al ver el campo seco?",
              options: ["Siguió de largo", "Se escondió asustada", "Empezó a llover", "Hizo mucho viento"],
              correctIndex: 2,
              hint: "¿Qué sucede cuando una nube se recarga de agua para refrescar un campo?"
            },
            {
              q: "¿De qué color se pusieron las plantas al final?",
              options: ["Amarillas", "Verdes", "Cafés", "Azules"],
              correctIndex: 1,
              hint: "Lee la cuarta oración. ¿Cómo cambiaron las plantitas al beber agua?"
            }
          ]
        }
      ],
      normal: [
        {
          id: "t3",
          level: "normal",
          levelName: "Normal 🐇",
          title: "La tortuga Catalina",
          body: "Catalina era una tortuga que soñaba con volar como los pájaros. Todos los días miraba el cielo y suspiraba. Un día, un águila le dijo: 'Yo te puedo enseñar a subir muy alto.' Catalina se aferró al cuello del águila y juntas subieron hasta las nubes. Cuando bajaron, Catalina entendió que no necesitaba alas para conocer el mundo, solo necesitaba buenos amigos.",
          word: "AMIGOS",
          wordHint: "Lo que la tortuga Catalina descubrió que era lo más importante para viajar.",
          questions: [
            {
              q: "¿Cuál era el gran sueño de Catalina?",
              options: ["Nadar en el mar azul", "Correr muy rápido", "Volar como los pájaros", "Ser muy famosa"],
              correctIndex: 2,
              hint: "¿Por qué miraba la tortuga Catalina al cielo suspirando todos los días?"
            },
            {
              q: "¿Qué animal ayudó a Catalina a subir alto?",
              options: ["Un tucán alegre", "Un águila fuerte", "Una mariposa", "Un búho sabio"],
              correctIndex: 1,
              hint: "¿Quién le propuso a Catalina enseñarle a subir hasta las nubes?"
            },
            {
              q: "¿Qué aprendió Catalina al final del viaje?",
              options: ["Que volar es muy peligroso", "Que necesita tener alas", "Que con buenos amigos se conoce el mundo", "Que prefiere dormir sola"],
              correctIndex: 2,
              hint: "Lee la última frase del cuento. ¿Qué valora Catalina al final?"
            }
          ]
        },
        {
          id: "t4",
          level: "normal",
          levelName: "Normal 🐇",
          title: "El mercado de don Félix",
          body: "Don Félix tiene un puesto de frutas en el mercado del pueblo. Cada mañana llega muy temprano a ordenar sus naranjas, mangos y piñas. Un martes, una niña llamada Rosa quiso comprar mangos, pero solo tenía la mitad del dinero. Don Félix la miró con amabilidad y le dijo: 'Llévate dos mangos hoy y la próxima semana me pagas.' Rosa sonrió y prometió volver.",
          word: "FRUTAS",
          wordHint: "Naranjas, mangos y piñas de don Félix son ejemplos de...",
          questions: [
            {
              q: "¿Qué vende don Félix en el mercado?",
              options: ["Verduras frescas", "Dulces y piñatas", "Frutas coloridas", "Ropa de niños"],
              correctIndex: 2,
              hint: "¿Qué deliciosos alimentos como naranjas y piñas organiza en su puesto?"
            },
            {
              q: "¿Por qué Rosa no podía pagar los mangos?",
              options: ["No le gustaba el precio", "Solo tenía la mitad del dinero", "El mercado estaba cerrado", "Perdió sus monedas"],
              correctIndex: 1,
              hint: "Revisa la conversación de Rosa con don Félix sobre el dinero que llevaba en su bolsa."
            },
            {
              q: "¿Qué valor demostró tener don Félix?",
              options: ["Enojo", "Amabilidad y confianza", "Prisa", "Desconfianza"],
              correctIndex: 1,
              hint: "¿Cómo reaccionó y qué le ofreció don Félix a la niña Rosa?"
            }
          ]
        }
      ],
      hard: [
        {
          id: "t5",
          level: "hard",
          levelName: "Difícil 🦅",
          title: "El río Claro y el bosque",
          body: "Había una vez un río llamado Claro que corría alegre entre las montañas. Pero un año de mucho calor, el río empezó a secarse poco a poco. Los peces buscaban sombra y los animales caminaban largas distancias para beber. Los habitantes decidieron sembrar árboles en las orillas. Con el tiempo, la sombra de los árboles refrescó el agua, y las lluvias volvieron a llenar el cauce. El río Claro aprendió que la naturaleza necesita el cuidado de todos.",
          word: "ARBOLES",
          wordHint: "Lo que sembraron los aldeanos en las orillas para refrescar el río con su sombra.",
          questions: [
            {
              q: "¿Por qué el río Claro comenzó a secarse?",
              options: ["Los peces bebían mucho", "Un año de calor extremo", "Construyeron una presa", "La gente tiró basura"],
              correctIndex: 1,
              hint: "Revisa la causa climática que afectó el flujo del agua al inicio de la historia."
            },
            {
              q: "¿Qué sembraron los vecinos en la orilla del río?",
              options: ["Flores coloridas", "Pasto sintético", "Árboles protectores", "Vegetales de huerto"],
              correctIndex: 2,
              hint: "¿Qué plantas de gran tamaño y tronco fuerte sembraron para crear sombra protectora?"
            },
            {
              q: "¿Cuál es la lección principal que nos enseña el cuento?",
              options: ["Los ríos no necesitan agua", "La naturaleza necesita el cuidado de todos", "Los peces viven sin sombra", "Los árboles secan los ríos"],
              correctIndex: 1,
              hint: "Vuelve a leer el hermoso mensaje que aprendió el río Claro en la última oración."
            }
          ]
        },
        {
          id: "t6",
          level: "hard",
          levelName: "Difícil 🦅",
          title: "La científica Valentina",
          body: "Valentina tenía nueve años y una libreta llena de preguntas. Quería saber por qué el cielo cambiaba de color al atardecer. Su maestra le explicó que la luz del sol viaja por el aire y choca con pequeñas partículas, y que dependiendo del ángulo, vemos distintos colores. Valentina no entendió todo de inmediato, pero escribió todo en su libreta y prometió seguir investigando. Esa noche, miró el cielo anaranjado y sonrió: cada pregunta era el inicio de un descubrimiento.",
          word: "CIENCIA",
          wordHint: "La pasión de Valentina por descubrir los secretos del universo y el cielo.",
          questions: [
            {
              q: "¿Qué duda misteriosa quería resolver Valentina?",
              options: ["Por qué llueve en invierno", "Por qué cambia el color del cielo", "Cómo vuelan los aviones", "De qué están hechas las estrellas"],
              correctIndex: 1,
              hint: "¿Qué miraba fijamente Valentina durante los atardeceres en su libreta de apuntes?"
            },
            {
              q: "¿Qué hacía Valentina con lo que no comprendía de inmediato?",
              options: ["Lo borraba enojada", "Lo guardaba en su memoria", "Lo anotaba en su libreta para investigar", "Se lo preguntaba a sus amigos"],
              correctIndex: 2,
              hint: "¿Cuál era la herramienta inseparable de Valentina donde guardaba sus preguntas?"
            },
            {
              q: "¿Qué representan las preguntas según la historia?",
              options: ["Un dolor de cabeza", "El inicio de un descubrimiento", "Una pérdida de tiempo", "Problemas difíciles"],
              correctIndex: 1,
              hint: "Lee la inspiradora frase final del cuento sobre el valor de ser curiosos."
            }
          ]
        }
      ]
    };

    /* ESTADO DEL JUEGO */
    let gameVars = {
      stars: 0,
      currentLevel: 'easy',
      currentStory: null,
      currentStage: 'setup', // setup, reading, quiz, wordbuilder, reflection, results
      timerInterval: null,
      timeLeft: 60,
      totalTime: 60,
      currentQuizIndex: 0,
      correctAnswersCount: 0,
      // Variables para el módulo Armar Palabras
      shuffledWordLetters: [],
      userWordLetters: [],
      wordBuilderSuccess: false
    };

    const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    
    function playBeep(type) {
      if (!audioCtx) return;
      
      const osc = audioCtx.createOscillator();
      const gain = audioCtx.createGain();
      osc.connect(gain);
      gain.connect(audioCtx.destination);
      
      if (type === 'success') {
        // Sonido ascendente alegre
        osc.frequency.setValueAtTime(523.25, audioCtx.currentTime); // C5
        osc.frequency.exponentialRampToValueAtTime(783.99, audioCtx.currentTime + 0.15); // G5
        gain.gain.setValueAtTime(0.15, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.25);
        osc.start();
        osc.stop(audioCtx.currentTime + 0.25);
      } else if (type === 'error') {
        // Sonido descendente grave
        osc.type = 'sawtooth';
        osc.frequency.setValueAtTime(220.00, audioCtx.currentTime); // A3
        osc.frequency.exponentialRampToValueAtTime(110.00, audioCtx.currentTime + 0.25); // A2
        gain.gain.setValueAtTime(0.15, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.3);
        osc.start();
        osc.stop(audioCtx.currentTime + 0.3);
      } else if (type === 'complete') {
        // Pequeña fanfarria triunfal
        const notes = [261.63, 329.63, 392.00, 523.25]; // C4, E4, G4, C5
        notes.forEach((freq, i) => {
          const noteOsc = audioCtx.createOscillator();
          const noteGain = audioCtx.createGain();
          noteOsc.connect(noteGain);
          noteGain.connect(audioCtx.destination);
          noteOsc.frequency.setValueAtTime(freq, audioCtx.currentTime + i * 0.12);
          noteGain.gain.setValueAtTime(0.12, audioCtx.currentTime + i * 0.12);
          noteGain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + i * 0.12 + 0.25);
          noteOsc.start(audioCtx.currentTime + i * 0.12);
          noteOsc.stop(audioCtx.currentTime + i * 0.12 + 0.25);
        });
      } else if (type === 'click') {
        // Clic de burbuja
        osc.type = 'sine';
        osc.frequency.setValueAtTime(600, audioCtx.currentTime);
        gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.08);
        osc.start();
        osc.stop(audioCtx.currentTime + 0.08);
      }
    }

    function switchTab(tab) {
      playBeep('click');
      const gameBtn = document.getElementById('btn-tab-game');
      const fichaBtn = document.getElementById('btn-tab-ficha');
      const gameSec = document.getElementById('section-game');
      const fichaSec = document.getElementById('section-ficha');

      if (tab === 'game') {
        gameBtn.classList.add('bg-white', 'text-blue-600', 'shadow-md');
        gameBtn.classList.remove('hover:bg-white/10', 'text-white');
        fichaBtn.classList.remove('bg-white', 'text-blue-600', 'shadow-md');
        fichaBtn.classList.add('hover:bg-white/10', 'text-white');
        
        gameSec.classList.remove('hidden');
        fichaSec.classList.add('hidden');
      } else {
        fichaBtn.classList.add('bg-white', 'text-blue-600', 'shadow-md');
        fichaBtn.classList.remove('hover:bg-white/10', 'text-white');
        gameBtn.classList.remove('bg-white', 'text-blue-600', 'shadow-md');
        gameBtn.classList.add('hover:bg-white/10', 'text-white');

        fichaSec.classList.remove('hidden');
        gameSec.classList.add('hidden');
      }
    }

    // Cambiar de fase dentro del juego
    function showGameStage(stageId) {
      gameVars.currentStage = stageId;
      document.getElementById('stage-setup').classList.add('hidden');
      document.getElementById('stage-reading').classList.add('hidden');
      document.getElementById('stage-quiz').classList.add('hidden');
      document.getElementById('stage-wordbuilder').classList.add('hidden');
      document.getElementById('stage-reflection').classList.add('hidden');
      document.getElementById('stage-results').classList.add('hidden');

      document.getElementById(`stage-${stageId}`).classList.remove('hidden');
    }

    function selectLevel(level) {
      playBeep('click');
      gameVars.currentLevel = level;
      
      // Cambiar temporizador según el nivel elegido
      if (level === 'easy') {
        gameVars.timeLeft = 60;
        document.getElementById('game-mascot').textContent = '🐢';
        document.getElementById('game-level-title').textContent = 'Nivel Fácil (Tortuga)';
        document.getElementById('game-header-bar').className = "bg-gradient-to-r from-emerald-400 to-teal-500 text-white p-4 flex justify-between items-center px-6";
      } else if (level === 'normal') {
        gameVars.timeLeft = 45;
        document.getElementById('game-mascot').textContent = '🐇';
        document.getElementById('game-level-title').textContent = 'Nivel Normal (Conejo)';
        document.getElementById('game-header-bar').className = "bg-gradient-to-r from-sky-400 to-blue-500 text-white p-4 flex justify-between items-center px-6";
      } else {
        gameVars.timeLeft = 30;
        document.getElementById('game-mascot').textContent = '🦅';
        document.getElementById('game-level-title').textContent = 'Nivel Difícil (Águila)';
        document.getElementById('game-header-bar').className = "bg-gradient-to-r from-rose-400 to-orange-500 text-white p-4 flex justify-between items-center px-6";
      }
      gameVars.totalTime = gameVars.timeLeft;

      // Seleccionar un cuento al azar de la base de datos
      const stories = database[level];
      const randomIndex = Math.floor(Math.random() * stories.length);
      gameVars.currentStory = stories[randomIndex];

      document.getElementById('game-text-indicator').textContent = `Texto: ${gameVars.currentStory.title}`;

      // Iniciar Fase de Lectura
      startReadingStage();
    }

    function startReadingStage() {
      showGameStage('reading');
      
      document.getElementById('reading-title').textContent = gameVars.currentStory.title;
      document.getElementById('reading-body').textContent = gameVars.currentStory.body;
      document.getElementById('timer-number').textContent = gameVars.timeLeft;
      
      const progressBar = document.getElementById('timer-progress-bar');
      progressBar.style.width = '100%';
      
      // Iniciar Intervalo del Temporizador
      if (gameVars.timerInterval) clearInterval(gameVars.timerInterval);
      
      gameVars.timerInterval = setInterval(() => {
        gameVars.timeLeft--;
        document.getElementById('timer-number').textContent = gameVars.timeLeft;
        
        const percent = (gameVars.timeLeft / gameVars.totalTime) * 100;
        progressBar.style.width = `${percent}%`;

        if (gameVars.timeLeft <= 10) {
          // Parpadear en rojo el temporizador en los últimos 10 segundos
          progressBar.classList.remove('from-teal-400', 'to-emerald-500');
          progressBar.classList.add('bg-rose-500');
        } else {
          progressBar.classList.remove('bg-rose-500');
          progressBar.classList.add('from-teal-400', 'to-emerald-500');
        }

        if (gameVars.timeLeft <= 0) {
          clearInterval(gameVars.timerInterval);
          playBeep('error');
          // Avanzar automáticamente por tiempo agotado
          startQuizStage();
        }
      }, 1000);
    }

    function finishReadingEarly() {
      if (gameVars.timerInterval) clearInterval(gameVars.timerInterval);
      playBeep('success');
      startQuizStage();
    }

    function startQuizStage() {
      gameVars.currentQuizIndex = 0;
      gameVars.correctAnswersCount = 0;
      showGameStage('quiz');
      loadQuizQuestion();
    }

    function loadQuizQuestion() {
      const story = gameVars.currentStory;
      const questionData = story.questions[gameVars.currentQuizIndex];
      
      // Actualizar progreso visual
      document.getElementById('quiz-index-indicator').textContent = `${gameVars.currentQuizIndex + 1}/3`;
      document.getElementById('quiz-question').textContent = questionData.q;
      
      // Ocultar caja de pista inicialmente
      document.getElementById('quiz-hint-box').classList.add('hidden');

      // Crear dots de progreso
      const dotsContainer = document.getElementById('quiz-dots');
      dotsContainer.innerHTML = '';
      for (let i = 0; i < 3; i++) {
        const dot = document.createElement('span');
        dot.className = `w-3 h-3 rounded-full transition-all duration-300 ${i < gameVars.currentQuizIndex ? 'bg-emerald-500' : 'bg-slate-200'}`;
        dotsContainer.appendChild(dot);
      }

      // Generar opciones
      const optionsContainer = document.getElementById('quiz-options-container');
      optionsContainer.innerHTML = '';

      questionData.options.forEach((opt, index) => {
        const button = document.createElement('button');
        button.className = "w-full p-4 bg-white hover:bg-slate-50 border-2 border-slate-200 text-slate-700 hover:border-slate-400 text-left font-semibold text-sm rounded-2xl transition-all-300 shadow-sm flex items-center justify-between";
        button.innerHTML = `
          <span>${opt}</span>
          <span class="text-xs bg-slate-100 text-slate-400 py-1 px-2.5 rounded-lg uppercase tracking-wider">Opción ${index + 1}</span>
        `;
        button.onclick = () => selectQuizOption(index, button);
        optionsContainer.appendChild(button);
      });
    }

    function selectQuizOption(selectedIndex, buttonElement) {
      const questionData = gameVars.currentStory.questions[gameVars.currentQuizIndex];
      const correctIdx = questionData.correctIndex;
      const optionsContainer = document.getElementById('quiz-options-container');
      const buttons = optionsContainer.getElementsByTagName('button');

      // Desactivar clics en las demás opciones
      for (let btn of buttons) {
        btn.disabled = true;
      }

      if (selectedIndex === correctIdx) {
        // RESPUESTA CORRECTA
        playBeep('success');
        buttonElement.className = "w-full p-4 bg-emerald-50 border-4 border-emerald-400 text-emerald-900 text-left font-bold text-sm rounded-2xl transition-all-300 shadow-md flex items-center justify-between";
        buttonElement.innerHTML += ` <span class="text-emerald-600 text-lg">🎉 ¡Correcto!</span>`;
        
        gameVars.correctAnswersCount++;
        gameVars.stars += 5;
        updateStarDisplay();

        // Esperar 1.8 segundos y pasar a la siguiente pregunta o fase
        setTimeout(() => {
          advanceQuiz();
        }, 1800);

      } else {
        // RESPUESTA INCORRECTA
        playBeep('error');
        buttonElement.className = "w-full p-4 bg-rose-50 border-4 border-rose-400 text-rose-900 text-left font-bold text-sm rounded-2xl transition-all-300 wobble flex items-center justify-between";
        buttonElement.innerHTML += ` <span class="text-rose-600 text-sm">❌ Intenta de nuevo</span>`;

        // Mostrar pista (Filtro didáctico, no se muestra respuesta)
        document.getElementById('quiz-hint-text').textContent = questionData.hint;
        document.getElementById('quiz-hint-box').classList.remove('hidden');

        // Permitir reintentar después de un momento corto de lectura de la pista
        setTimeout(() => {
          for (let btn of buttons) {
            if (btn !== buttonElement) {
              btn.disabled = false;
            }
          }
        }, 1500);
      }
    }

    function advanceQuiz() {
      gameVars.currentQuizIndex++;
      if (gameVars.currentQuizIndex < 3) {
        loadQuizQuestion();
      } else {
        // Al terminar las preguntas, pasar al NUEVO juego interactivo "Armar Palabras"
        startWordBuilderStage();
      }
    }

    function startWordBuilderStage() {
      showGameStage('wordbuilder');
      
      const story = gameVars.currentStory;
      const targetWord = story.word.toUpperCase();
      
      document.getElementById('wordbuilder-hint').textContent = `"${story.wordHint}"`;
      
      // Preparar arreglos de estado
      gameVars.shuffledWordLetters = targetWord.split('');
      // Desordenar las letras
      shuffleArray(gameVars.shuffledWordLetters);
      // Evitar que queden idénticas a la palabra original si es muy corta
      if (gameVars.shuffledWordLetters.join('') === targetWord) {
        gameVars.shuffledWordLetters.reverse();
      }

      gameVars.userWordLetters = Array(targetWord.length).fill(null);
      gameVars.wordBuilderSuccess = false;

      renderWordBuilder();
    }

    // Algoritmo Fisher-Yates para desordenar
    function shuffleArray(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
    }

    function renderWordBuilder() {
      const slotsContainer = document.getElementById('wordbuilder-slots');
      const poolContainer = document.getElementById('wordbuilder-pool');

      slotsContainer.innerHTML = '';
      poolContainer.innerHTML = '';

      // 1. Dibujar los Slots de Destino (Casillas que el niño va llenando)
      gameVars.userWordLetters.forEach((letter, index) => {
        const slot = document.createElement('div');
        if (letter === null) {
          slot.className = "w-12 h-12 md:w-14 md:h-14 border-4 border-dashed border-slate-300 rounded-xl bg-slate-50 flex items-center justify-center font-kids text-xl md:text-2xl text-slate-400 transition-all-300";
          slot.textContent = "?";
        } else {
          slot.className = "w-12 h-12 md:w-14 md:h-14 border-4 border-violet-400 bg-violet-100 rounded-xl flex items-center justify-center font-kids text-xl md:text-2xl text-violet-900 cursor-pointer shadow hover:scale-105 transition-all-300";
          slot.textContent = letter;
          // Si el niño cliquea una letra puesta, la remueve
          slot.onclick = () => removeLetterFromSlot(index);
        }
        slotsContainer.appendChild(slot);
      });

      // 2. Dibujar la alberca de letras de origen disponibles
      gameVars.shuffledWordLetters.forEach((letter, index) => {
        const button = document.createElement('button');
        if (letter === null) {
          // Letra ya usada
          button.className = "w-12 h-12 md:w-14 md:h-14 bg-slate-100 text-slate-200 border-2 border-slate-200 rounded-xl font-kids text-xl md:text-2xl cursor-not-allowed opacity-40 transition-all-300";
          button.textContent = "";
          button.disabled = true;
        } else {
          // Letra libre para cliquear
          button.className = "w-12 h-12 md:w-14 md:h-14 bg-amber-400 hover:bg-amber-300 text-slate-900 border-4 border-white rounded-xl font-kids text-xl md:text-2xl shadow-md hover:shadow-lg hover:-translate-y-1 active:translate-y-0 transition-all-300";
          button.textContent = letter;
          button.onclick = () => addLetterToSlot(letter, index);
        }
        poolContainer.appendChild(button);
      });
    }

    function addLetterToSlot(letter, originalPoolIndex) {
      playBeep('click');
      // Buscar el primer slot vacío
      const emptyIndex = gameVars.userWordLetters.indexOf(null);
      if (emptyIndex !== -1) {
        gameVars.userWordLetters[emptyIndex] = letter;
        // Marcar la letra como usada en el pool
        gameVars.shuffledWordLetters[originalPoolIndex] = null;
        renderWordBuilder();
      }
    }

    function removeLetterFromSlot(slotIndex) {
      playBeep('click');
      const letter = gameVars.userWordLetters[slotIndex];
      if (letter !== null) {
        // Remover del slot
        gameVars.userWordLetters[slotIndex] = null;
        // Regresar la letra al primer espacio nulo del pool de origen
        const emptyPoolIndex = gameVars.shuffledWordLetters.indexOf(null);
        if (emptyPoolIndex !== -1) {
          gameVars.shuffledWordLetters[emptyPoolIndex] = letter;
        } else {
          gameVars.shuffledWordLetters.push(letter);
        }
        renderWordBuilder();
      }
    }

    function resetWordBuilder() {
      playBeep('click');
      startWordBuilderStage();
    }

    function checkWordBuilderSolution() {
      const targetWord = gameVars.currentStory.word.toUpperCase();
      const userWord = gameVars.userWordLetters.join('');

      if (userWord === targetWord) {
        // ¡PALABRA CORRECTA!
        playBeep('complete');
        gameVars.wordBuilderSuccess = true;
        gameVars.stars += 15;
        updateStarDisplay();

        const slotsContainer = document.getElementById('wordbuilder-slots');
        // Marcar todos los bloques de verde feliz
        for (let child of slotsContainer.children) {
          child.className = "w-12 h-12 md:w-14 md:h-14 bg-emerald-500 border-4 border-white text-white rounded-xl flex items-center justify-center font-kids text-xl md:text-2xl shadow-lg transition-all-300 scale-110";
        }

        setTimeout(() => {
          // Pasar a fase de reflexión escrita
          startReflectionStage();
        }, 1800);

      } else {
        // ERROR EN PALABRA
        playBeep('error');
        const slotsContainer = document.getElementById('wordbuilder-slots');
        // Wobble y marcar temporalmente de rojo
        for (let child of slotsContainer.children) {
          child.classList.add('wobble', 'border-rose-500', 'bg-rose-50');
        }
        setTimeout(() => {
          for (let child of slotsContainer.children) {
            child.classList.remove('wobble', 'border-rose-500', 'bg-rose-50');
          }
        }, 400);
      }
    }

    function startReflectionStage() {
      showGameStage('reflection');
      document.getElementById('reflection-textarea').value = '';
      validateReflection();
    }

    function validateReflection() {
      const text = document.getElementById('reflection-textarea').value.trim();
      const countLabel = document.getElementById('reflection-char-count');
      const submitBtn = document.getElementById('btn-submit-reflection');

      countLabel.textContent = `${text.length} / 15 caracteres mínimos`;

      if (text.length >= 15) {
        countLabel.className = "text-emerald-600 font-bold";
        submitBtn.className = "bg-gradient-to-r from-emerald-500 to-teal-600 text-white font-kids text-lg px-10 py-3.5 rounded-2xl cursor-pointer hover:scale-105 active:scale-95 shadow-md transition-all-300";
        submitBtn.disabled = false;
      } else {
        countLabel.className = "text-slate-400 font-semibold";
        submitBtn.className = "bg-slate-300 text-slate-500 font-kids text-lg px-10 py-3.5 rounded-2xl cursor-not-allowed transition-all-300";
        submitBtn.disabled = true;
      }
    }

    function submitReflection() {
      playBeep('complete');
      gameVars.stars += 10;
      updateStarDisplay();
      showResultsStage();
    }

    function showResultsStage() {
      showGameStage('results');
      
      const starsDisplay = document.getElementById('stat-stars');
      const quizDisplay = document.getElementById('stat-quiz');
      const reflectionText = document.getElementById('result-reflection-text');

      starsDisplay.textContent = gameVars.stars;
      quizDisplay.textContent = `${gameVars.correctAnswersCount}/3`;
      reflectionText.textContent = `"${document.getElementById('reflection-textarea').value.trim()}"`;

      // Definir carita y mensaje basado en respuestas de comprensión
      const emoji = document.getElementById('result-emoji');
      const title = document.getElementById('result-title');
      const subtitle = document.getElementById('result-subtitle');

      if (gameVars.correctAnswersCount >= 2) {
        emoji.textContent = "😄";
        title.textContent = "¡Campeón de la Comprensión! 🏆";
        subtitle.textContent = "¡Increíble! Has comprendido el cuento de forma perfecta y completaste la palabra.";
      } else {
        emoji.textContent = "🙂";
        title.textContent = "¡Buen Intento, Explorador!";
        subtitle.textContent = "Recuerda que leer no es solo pronunciar palabras rápidamente, ¡sino recordar los detalles de la historia!";
      }
    }

    function updateStarDisplay() {
      document.getElementById('star-count').textContent = gameVars.stars;
    }

    function retryCurrentLevel() {
      playBeep('click');
      selectLevel(gameVars.currentLevel);
    }

    function resetToSetup() {
      playBeep('click');
      showGameStage('setup');
      document.getElementById('game-text-indicator').textContent = "Selecciona un nivel";
    }

    function renderTeacherPanel() {
      const container = document.getElementById('editor-texts-container');
      container.innerHTML = '';

      const levels = ['easy', 'normal', 'hard'];
      const badgesClasses = {
        easy: "bg-emerald-100 text-emerald-800",
        normal: "bg-sky-100 text-sky-800",
        hard: "bg-rose-100 text-rose-800"
      };

      levels.forEach(lvl => {
        database[lvl].forEach((story, sIndex) => {
          const card = document.createElement('div');
          card.className = "p-5 border-2 border-slate-200 rounded-2xl space-y-4 bg-slate-50 relative hover:border-slate-300 transition-all-300";
          card.innerHTML = `
            <span class="absolute -top-3.5 right-4 px-3 py-1 rounded-full text-[10px] font-bold uppercase tracking-wider ${badgesClasses[lvl]}">
              ${story.levelName}
            </span>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div>
                <label class="block text-[11px] font-bold text-slate-500 mb-1">Título del Cuento</label>
                <input type="text" value="${story.title}" onchange="updateDatabaseField('${lvl}', ${sIndex}, 'title', this.value)" class="w-full border rounded-lg p-2 text-xs font-semibold bg-white">
              </div>
              <div class="grid grid-cols-2 gap-2">
                <div>
                  <label class="block text-[11px] font-bold text-slate-500 mb-1">Palabra Clave (Minijuego)</label>
                  <input type="text" value="${story.word}" onchange="updateDatabaseField('${lvl}', ${sIndex}, 'word', this.value.toUpperCase().trim())" class="w-full border rounded-lg p-2 text-xs font-bold text-violet-700 bg-white uppercase">
                </div>
                <div>
                  <label class="block text-[11px] font-bold text-slate-500 mb-1">Pista de la Palabra</label>
                  <input type="text" value="${story.wordHint}" onchange="updateDatabaseField('${lvl}', ${sIndex}, 'wordHint', this.value)" class="w-full border rounded-lg p-2 text-xs font-semibold bg-white">
                </div>
              </div>
            </div>

            <div>
              <label class="block text-[11px] font-bold text-slate-500 mb-1">Cuerpo del Cuento</label>
              <textarea onchange="updateDatabaseField('${lvl}', ${sIndex}, 'body', this.value)" class="w-full border rounded-lg p-2 text-xs font-medium bg-white min-h-[70px] leading-relaxed">${story.body}</textarea>
            </div>

            <!-- Editor de Preguntas -->
            <div class="space-y-3 pt-2 border-t border-dashed border-slate-200">
              <h5 class="text-xs font-bold text-slate-600 flex items-center gap-1">📋 Preguntas de Comprensión:</h5>
              
              <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                ${story.questions.map((qData, qIndex) => `
                  <div class="p-3 bg-white border rounded-xl space-y-2 relative shadow-sm">
                    <span class="text-[10px] font-bold text-cyan-600 block mb-1">Pregunta ${qIndex + 1}</span>
                    <input type="text" value="${qData.q}" onchange="updateDatabaseQuestionField('${lvl}', ${sIndex}, ${qIndex}, 'q', this.value)" class="w-full border p-1.5 text-xs font-bold rounded">
                    
                    <div class="space-y-1">
                      <label class="text-[9px] font-bold text-slate-400 block">Opciones:</label>
                      ${qData.options.map((opt, oIndex) => `
                        <div class="flex items-center gap-1.5">
                          <input type="radio" name="correct-${lvl}-${sIndex}-${qIndex}" ${qData.correctIndex === oIndex ? 'checked' : ''} onchange="updateDatabaseQuestionField('${lvl}', ${sIndex}, ${qIndex}, 'correctIndex', ${oIndex})" class="accent-emerald-500">
                          <input type="text" value="${opt}" onchange="updateDatabaseQuestionOption('${lvl}', ${sIndex}, ${qIndex}, ${oIndex}, this.value)" class="w-full border p-1 text-[11px] font-semibold rounded ${qData.correctIndex === oIndex ? 'border-emerald-300 bg-emerald-50/50' : ''}">
                        </div>
                      `).join('')}
                    </div>

                    <div>
                      <label class="text-[9px] font-bold text-slate-400 block">Pregunta de Andamiaje (Pista):</label>
                      <input type="text" value="${qData.hint}" onchange="updateDatabaseQuestionField('${lvl}', ${sIndex}, ${qIndex}, 'hint', this.value)" class="w-full border p-1 text-[10px] bg-amber-50 rounded">
                    </div>
                  </div>
                `).join('')}
              </div>
            </div>
          `;
          container.appendChild(card);
        });
      });
    }

    function updateDatabaseField(level, index, field, value) {
      database[level][index][field] = value;
    }

    function updateDatabaseQuestionField(level, sIndex, qIndex, field, value) {
      database[level][sIndex].questions[qIndex][field] = value;
    }

    function updateDatabaseQuestionOption(level, sIndex, qIndex, oIndex, value) {
      database[level][sIndex].questions[qIndex].options[oIndex] = value;
    }

    function syncFichaToGame() {
      playBeep('complete');
      
      // Sincronizar las variables con la UI de juego activa
      if (gameVars.currentStory) {
        // Encontrar la historia en la base de datos actualizada
        const updatedStory = database[gameVars.currentLevel].find(s => s.id === gameVars.currentStory.id);
        if (updatedStory) {
          gameVars.currentStory = updatedStory;
        }
      }

      // Reiniciar visuales
      resetToSetup();
      
      // Mostrar feedback amigable de guardado
      const alertBox = document.createElement('div');
      alertBox.className = "fixed top-5 right-5 bg-gradient-to-r from-emerald-500 to-teal-600 text-white font-kids p-4 rounded-2xl shadow-xl z-50 text-xs flex items-center gap-2 transform translate-y-0 transition-all duration-500";
      alertBox.innerHTML = `<span>✨ ¡Simulador Sincronizado Correctamente! ✨</span>`;
      document.body.appendChild(alertBox);

      setTimeout(() => {
        alertBox.classList.add('opacity-0', 'translate-y-[-20px]');
        setTimeout(() => alertBox.remove(), 500);
      }, 2500);

      // Regresar al modo juego automáticamente para que los niños experimenten los cambios
      switchTab('game');
    }

    /* CONTROL DE CHECKLIST */
    function toggleCheckItem(li) {
      const cb = li.querySelector('input[type="checkbox"]');
      cb.checked = !cb.checked;
      updateCheckStatus();
    }

    function updateCheckStatus() {
      const items = document.querySelectorAll('#checklist li');
      let checkedCount = 0;
      items.forEach(item => {
        const cb = item.querySelector('input[type="checkbox"]');
        if (cb.checked) checkedCount++;
      });

      const label = document.getElementById('check-status');
      if (checkedCount === items.length) {
        label.textContent = `✅ ¡Ficha Pedagógica de Codiseño lista! (${checkedCount}/${items.length} criterios cumplidos)`;
        label.className = "mt-4 text-xs font-bold text-emerald-600";
      } else {
        label.textContent = `⚠️ Criterios validados: ${checkedCount} de ${items.length} totales. Completa todos los campos para finalizar el taller.`;
        label.className = "mt-4 text-xs font-bold text-amber-600";
      }
    }

    // Inicializar al cargar la página
    window.onload = function() {
      // Ajustar fecha por defecto a hoy
      const dateInput = document.getElementById('teacher-date');
      if (dateInput) {
        const today = new Date().toISOString().split('T')[0];
        dateInput.value = today;
      }
      
      // Renderizar el panel del profesor
      renderTeacherPanel();
      updateCheckStatus();
    };
  </script>
</body>
</html>
