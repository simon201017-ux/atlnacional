<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Atlético Nacional 🟢⚪ — SPA & Timeline</title>
  <link rel="icon" href="favicon.png" type="image/png">
  <style>
    :root{
      --verde:#0f5b28;
      --verde-2:#00a65a;
      --fondo:#0b0b0b;
      --panel:#0f1210;
      --texto:#e9f0ec;
      --muted:#9aa69a;
      --accent:#bfead0;
      --glass: rgba(255,255,255,0.03);
    }
    *{box-sizing:border-box;margin:0;padding:0}
    html,body{height:100%}
    body{
      font-family: Inter, 'Segoe UI', Roboto, Arial, sans-serif;
      background: linear-gradient(180deg,#050505 0%, #0b0b0b 100%);
      color:var(--texto);
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      line-height:1.45;
      padding-bottom:40px;document.getElementById('limpiar-seleccion').addEventListener('click', clearSelection);

    }

    header{
      display:flex;align-items:center;gap:14px;padding:12px 18px;background:linear-gradient(90deg,var(--verde),var(--verde-2));
      box-shadow:0 6px 24px rgba(0,0,0,0.5);position:sticky;top:0;z-index:50
    }
    .brand{display:flex;align-items:center;gap:12px}
    .brand img{width:56px;height:56px;border-radius:8px;object-fit:cover;box-shadow:0 6px 18px rgba(0,0,0,0.4)}
    .brand h1{font-size:18px;color:#fff;margin:0}

    nav{display:flex;gap:10px;justify-content:center;padding:10px 12px;background:var(--panel);position:sticky;top:68px;z-index:40}
    nav button{background:transparent;border:2px solid rgba(255,255,255,0.06);color:var(--texto);padding:8px 12px;border-radius:10px;cursor:pointer;font-weight:700;transition:all .28s}
    nav button:hover{transform:translateY(-3px);box-shadow:0 6px 18px rgba(0,0,0,0.6)}
    nav button.active{background:var(--verde);color:#07110a;border-color:transparent}

    .wrap{max-width:1100px;margin:20px auto;padding:0 16px}
    .section{display:none;opacity:0;transform:translateY(8px);transition:opacity .45s ease,transform .45s ease;}
    .section.active{display:block;opacity:1;transform:translateY(0)}

    .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border:1px solid rgba(255,255,255,0.03);padding:18px;border-radius:12px;box-shadow:0 8px 30px rgba(0,0,0,0.6);margin-bottom:20px}
    h2{color:var(--verde);margin-bottom:10px}
    p.lead{color:var(--muted);margin-bottom:10px}
    img.responsive{width:100%;border-radius:10px;margin-top:12px}

    table{width:100%;border-collapse:collapse;margin-top:10px}
    th,td{padding:10px;border-bottom:1px solid rgba(255,255,255,0.03)}
    th{color:var(--accent);text-align:left}

    footer{max-width:1100px;margin:18px auto;text-align:center;color:var(--muted);padding:12px}

    /* Timeline style 2 - interactive */
    .timeline{
      position:relative;padding:18px 8px 8px 26px;overflow:visible
    }
    .timeline::before{
      content:"";position:absolute;left:14px;top:8px;bottom:8px;width:4px;background:linear-gradient(180deg,var(--verde),var(--verde-2));border-radius:4px;opacity:0.9
    }
    .event{
      position:relative;margin:22px 0;padding:12px 18px;border-radius:10px;background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.02));border:1px solid var(--glass);box-shadow:0 8px 30px rgba(0,0,0,0.45);transform:translateX(18px);opacity:0;transition:all .6s cubic-bezier(.2,.9,.2,1);
    }
    .event.visible{transform:none;opacity:1}
    .event .dot{position:absolute;left:-34px;top:14px;width:24px;height:24px;border-radius:50%;background:var(--verde-2);display:flex;align-items:center;justify-content:center;font-weight:900;color:#07110a;box-shadow:0 6px 18px rgba(0,0,0,0.5)}
    .event h3{margin-bottom:6px;color:var(--accent)}
    .event p{color:var(--muted);margin-bottom:6px}
    .marker{font-weight:900;color:var(--verde-2);margin-right:8px}
    .quote{display:block;padding:10px;border-left:3px solid rgba(191,234,208,0.18);margin-top:8px;color:var(--texto);background:rgba(255,255,255,0.01);border-radius:6px}
    .small{font-size:0.9rem;color:var(--muted)}

    /* Sopa styles (kept from original) */
    .sopa-controls{display:flex;gap:8px;justify-content:center;margin:12px 0}
    .btn{background:var(--verde);color:#07110a;border:none;padding:8px 12px;border-radius:8px;cursor:pointer;font-weight:700}
    .btn.secondary{background:#2b2b2b;color:var(--texto)}
    .sopa-wrap{display:flex;gap:18px;flex-wrap:wrap;align-items:flex-start;justify-content:center}
    .grid{display:grid;grid-template-columns:repeat(12,36px);gap:6px;justify-content:center}
    .cell{width:36px;height:36px;background:#121212;color:var(--texto);display:flex;align-items:center;justify-content:center;font-weight:800;border-radius:6px;cursor:pointer;user-select:none;transition:transform .12s,background .12s}
    .cell.sel{background:var(--verde);color:#07110a}
    .cell.found{background:#cfead5;color:#07110a;text-decoration:line-through}
    .words{display:flex;gap:8px;flex-wrap:wrap;justify-content:center;margin-top:8px}
    .words .word{padding:6px 10px;border-radius:8px;background:rgba(255,255,255,0.03);border:1px solid rgba(255,255,255,0.03);font-weight:700;color:var(--accent)}
    .words .word.found{background:linear-gradient(90deg,#ddf5e6,#cfead5);color:var(--verde);text-decoration:line-through;border-color:var(--verde)}

    /* Responsive */
    @media (max-width:880px){.grid{grid-template-columns:repeat(10,32px)}.cell{width:32px;height:32px}}
    @media (max-width:720px){header{padding:10px}nav{top:62px} .brand img{width:48px;height:48px} .brand h1{font-size:16px}}
    @media (max-width:560px){.grid{grid-template-columns:repeat(8,30px)}.cell{width:30px;height:30px}.timeline{padding-left:18px}.timeline::before{left:10px}.event{transform:translateX(8px)}.event .dot{left:-30px}}
  </style>
</head>
<body>

  <header>
    <div class="brand">
      <img src="https://pbs.twimg.com/profile_images/805888972304093189/W09uqRA6_400x400.jpg" alt="Escudo Atlético Nacional">
      <h1>Atlético Nacional — Sitio Interactivo</h1>
    </div>
  </header>

  <nav>
    <button data-section="inicio">Inicio</button>
    <button data-section="historia" class="active">Historia</button>
    <button data-section="timeline">Timeline</button>
    <button data-section="formulario">Cuestionario</button>
    <button data-section="sopa">Sopa de letras</button>
  </nav>

  <main class="wrap">

    <section id="inicio" class="section">
      <div class="card">
        <h2>Bienvenido Verdolaga 💚</h2>
        <p class="lead">Explora la historia, demuestra tus conocimientos con el cuestionario y disfruta de la sopa de letras interactiva — todo en una sola página.</p>
         <img class="responsive" src="https://i0.wp.com/stadiumbase.com/wp-content/uploads/2020/05/Estadio-Atanasio-Girardot5.png?fit=900%2C600&ssl=1" alt="Estadio Atanasio Girardot">
      </div>
    </section>

    <section id="historia" class="section active">
      <!-- Mantengo una versión resumida de la historia original para compatibilidad -->
      <div class="card">
        <h2>Historia del Club</h2>
        <p class="lead">Fundado en 1947 en Medellín, Atlético Nacional se consolidó como uno de los clubes más importantes de Colombia y Sudamérica. A través de décadas, ha vivido épocas de gloria, crisis y renacimiento que han marcado su carácter y su relación con la ciudad.</p>
        <img class="responsive" src="https://i0.wp.com/stadiumbase.com/wp-content/uploads/2020/05/Estadio-Atanasio-Girardot5.png?fit=900%2C600&ssl=1" alt="Estadio Atanasio Girardot">
      </div>

      <div class="card">
        <h2>Identidad y Filosofía</h2>
        <p class="lead">La identidad verdolaga nace de Medellín: trabajo, garra y una identidad colectiva fuerte. El club promueve el juego ofensivo, la formación de jóvenes y una relación estrecha con sus hinchas.</p>
      </div>

      <div class="card">
        <h2>Palmarés y Logros</h2>
        <table>
          <thead><tr><th>Competición</th><th>Títulos</th></tr></thead>
          <tbody>
            <tr><td>Liga Colombiana</td><td>16</td></tr>
            <tr><td>Copa Colombia</td><td>3</td></tr>
            <tr><td>Copa Libertadores</td><td>2</td></tr>
            <tr><td>Superliga</td><td>1</td></tr>
          </tbody>
        </table>
      </div>

    </section>

    <!-- TIMELINE (nuevo) -->
    <section id="timeline" class="section">
      <div class="card">
        <h2>Timeline: Atlético Nacional en el fútbol colombiano</h2>
        <p class="lead">(Enfoque: impacto, estilo de juego y legado). Desplázate para ver hitos y citas.</p>

        <div class="timeline" id="timelineList">

          <article class="event" data-delay="0">
            <span class="dot">●</span>
            <h3>I. INTRODUCCIÓN</h3>
            <p class="small"><span class="marker">➤</span>Atlético Nacional es uno de los clubes más influyentes en la historia del fútbol colombiano, no solo por su vitrina deportiva sino por la construcción de una identidad que combina competitividad, formación de talento propio y proyección internacional.</p>
            <p class="quote">“Nacional no solo compite: marca tendencia dentro y fuera de Colombia.”</p>
          </article>

          <article class="event" data-delay="80">
            <span class="dot">●</span>
            <h3>II. CONTEXTO HISTÓRICO — Fundación y consolidación</h3>
            <p class="small"><span class="marker">➤</span><strong>1947 — Fundación:</strong> Nace como Club Atlético Municipal. Desde sus primeros años apuesta por futbolistas nacionales y la formación juvenil.</p>
            <p class="small"><span class="marker">➤</span><strong>1960–1970 — Crecimiento:</strong> Consolidación en el plano nacional; refuerzo del trabajo de filiales y academias.</p>
            <p class="small"><span class="marker">➤</span><strong>1989 — Hito mayor:</strong> Copa Libertadores 1989 (primer club colombiano en ganar la Libertadores), hecho que impulsó la proyección internacional del fútbol colombiano.</p>
          </article>

          <article class="event" data-delay="160">
            <span class="dot">●</span>
            <h3>III. DESARROLLO — Modelo, cantera y títulos</h3>
            <p class="small"><span class="marker">➤</span><strong>Modelo futbolístico:</strong> Priorización del trato de balón, salida desde el fondo y juego ofensivo; esto generó una "escuela" reconocida en el país.</p>
            <p class="small"><span class="marker">➤</span><strong>Cantera:</strong> Formó jugadores para la selección y el mercado internacional, consolidando una política de sostenibilidad deportiva.</p>
            <p class="small"><span class="marker">➤</span><strong>2016 — Renovación continental:</strong> Copa Libertadores 2016, reafirmando la vigencia del proyecto deportivo.</p>

            <p class="quote">"Atlético Nacional es el club que mejor interpreta el fútbol moderno en Sudamérica." — <em>FOX Sports</em></p>
            <p class="quote">"Nacional no solo juega bien: enseña cómo se debe jugar." — <em>Reinaldo Rueda</em></p>
          </article>

          <article class="event" data-delay="240">
            <span class="dot">●</span>
            <h3>IV. IMPACTO Y LEGADO</h3>
            <p class="small"><span class="marker">➤</span>El club elevó los estándares tácticos y formativos del fútbol colombiano, promoviendo la profesionalización de divisiones menores y la exportación de talento.</p>
            <p class="small"><span class="marker">➤</span>En el plano institucional, el club se convirtió en referente administrativo y organizativo para otros equipos en Colombia.</p>
          </article>

          <article class="event" data-delay="320">
            <span class="dot">●</span>
            <h3>V. CONCLUSIÓN (PERSPECTIVA HISTORIADOR)</h3>
            <p class="small"><span class="marker">➤</span>Atlético Nacional no es solo un ganador de torneos: es un arquitecto de identidad futbolística en Colombia. Su influencia perdura en la formación de jugadores, el estilo de juego y la manera en que el fútbol colombiano se proyecta internacionalmente.</p>
            <p class="quote">"En términos históricos, Nacional actuó como agente transformador dentro del deporte colombiano."</p>
          </article>

        </div>
      </div>
    </section>

    <!-- FORMULARIO (se mantiene, con mejora de almacenamiento opcional) -->
    <section id="formulario" class="section">
      <div class="card">
        <h2>Cuestionario sobre Atlético Nacional 🟢⚪</h2>
        <form id="quiz" autocomplete="off">
          <fieldset style="border:1px solid rgba(255,255,255,0.04);padding:12px;border-radius:8px;margin-bottom:12px">
            <legend style="color:var(--accent);font-weight:800">Preguntas (10)</legend>

            <p><strong>1.</strong> ¿En qué año fue fundado Atlético Nacional?</p>
            <label><input type="radio" name="fundacion" value="1947"> 1947</label><br>
            <label><input type="radio" name="fundacion" value="1950"> 1950</label><br>
            <label><input type="radio" name="fundacion" value="1935"> 1935</label>

            <p><strong>2.</strong> ¿Dónde juega sus partidos como local?</p>
            <label><input type="radio" name="estadio" value="Atanasio"> Estadio Atanasio Girardot</label><br>
            <label><input type="radio" name="estadio" value="Campin"> Estadio El Campín</label><br>

            <p><strong>3.</strong> ¿Cuál es el apodo del equipo?</p>
            <label><input type="radio" name="apodo" value="Verdolagas"> Verdolagas</label><br>
            <label><input type="radio" name="apodo" value="Tiburones"> Tiburones</label><br>

            <p><strong>4.</strong> ¿Cuántas Copas Libertadores ha ganado?</p>
            <select name="libertadores">
              <option value="">Selecciona...</option>
              <option value="1">1</option>
              <option value="2">2</option>
              <option value="3">3</option>
            </select>

            <p><strong>5.</strong> ¿Quién fue el entrenador en 2016?</p>
            <select name="entrenador">
              <option value="">Selecciona...</option>
              <option value="Rueda">Reinaldo Rueda</option>
              <option value="Osorio">Juan Carlos Osorio</option>
              <option value="Gomez">Hernán Darío Gómez</option>
            </select>

            <p><strong>6.</strong> ¿Cuál es su clásico rival?</p>
            <select name="rival">
              <option value="">Selecciona...</option>
              <option value="DIM">Independiente Medellín</option>
              <option value="Millonarios">Millonarios</option>
              <option value="America">América de Cali</option>
            </select>

            <p><strong>7.</strong> Jugador favorito actual:</p>
            <input type="text" name="jugador_favorito" placeholder="Nombre del jugador" style="width:100%;padding:8px;border-radius:6px;border:1px solid rgba(255,255,255,0.04);background:#080808;color:var(--texto)">

            <p><strong>8.</strong> ¿En qué ciudad se fundó el club?</p>
            <input type="text" name="ciudad_fundacion" placeholder="Ciudad" style="width:100%;padding:8px;border-radius:6px;border:1px solid rgba(255,255,255,0.04);background:#080808;color:var(--texto)">

            <p><strong>9.</strong> ¿Por qué apoyas a Atlético Nacional? (breve)</p>
            <textarea name="razon" rows="3" style="width:100%;padding:8px;border-radius:6px;border:1px solid rgba(255,255,255,0.04);background:#080808;color:var(--texto)"></textarea>

            <p><strong>10.</strong> Jugadores históricos favoritos (marca varios):</p>
            <label><input type="checkbox" name="historia" value="Higuita"> René Higuita</label><br>
            <label><input type="checkbox" name="historia" value="Aristizabal"> Víctor Aristizábal</label><br>
            <label><input type="checkbox" name="historia" value="Escobar"> Andrés Escobar</label><br>
            <label><input type="checkbox" name="historia" value="Macnelly"> Macnelly Torres</label><br>

          </fieldset>

          <div style="display:flex;gap:8px;justify-content:flex-end">
            <button type="reset" class="btn secondary" style="border:1px solid rgba(255,255,255,0.04)">Restablecer</button>
            <button type="submit" class="btn">Enviar respuestas</button>
          </div>
        </form>

        <div id="quizResult" style="margin-top:12px;display:none" class="card"></div>
      </div>
    </section>

    <!-- SOPA -->
    <section id="sopa" class="section">
      <div class="card">
        <h2>Sopa de letras — Atlético Nacional</h2>

        <div class="sopa-controls">
          <button id="recrear" class="btn">🔄 Reiniciar sopa</button>
          <button id="mostrar" class="btn secondary">👀 Mostrar solución</button>
          <button id="limpiar" class="btn secondary">🧹 Limpiar selección</button>
        </div>

        <div class="sopa-wrap">
          <div id="grid" class="grid" aria-hidden="false"></div>
        </div>

        <div class="words" id="wordList"></div>
        <p style="text-align:center;color:var(--muted);margin-top:10px">Selecciona arrastrando o haciendo clic para formar las palabras. Las palabras se generan aleatoriamente cada vez que presionas "Reiniciar sopa".</p>
      </div>
    </section>

  </main>

  <footer>
    <p>Atlético Nacional – Orgullo Verdolaga 💚⚪ — por SIMÓN ZAPATA & JHORBAN MOSQUERA</p>
  </footer>

  <script>
    /* ---------- SPA NAV ---------- */
    const navButtons = document.querySelectorAll('nav button');
    const sections = document.querySelectorAll('.section');
    function showSection(id){
      sections.forEach(s=>{
        if(s.id===id){ s.classList.add('active'); }
        else s.classList.remove('active');
      });
      navButtons.forEach(b=>b.classList.toggle('active', b.dataset.section===id));
      window.scrollTo({top:0,behavior:'smooth'});
    }
    navButtons.forEach(b=>b.addEventListener('click', ()=> showSection(b.dataset.section)));

    /* ---------- QUIZ: corrección y localStorage ---------- */
    const correctAnswers = {
      fundacion: '1947',
      estadio: 'Atanasio',
      apodo: 'Verdolagas',
      libertadores: '2', // valor por defecto asumido en select
      entrenador: 'Rueda',
      rival: 'DIM'
    };

    const quizEl = document.getElementById('quiz');
    const resultEl = document.getElementById('quizResult');

    quizEl.addEventListener('submit', function(e){
      e.preventDefault();
      const data = new FormData(this);
      let score = 0; let total = 6; // contamos solo preguntas objetivas
      if(data.get('fundacion')===correctAnswers.fundacion) score++;
      if(data.get('estadio')===correctAnswers.estadio) score++;
      if(data.get('apodo')===correctAnswers.apodo) score++;
      if(data.get('libertadores')===correctAnswers.libertadores) score++;
      if(data.get('entrenador')===correctAnswers.entrenador) score++;
      if(data.get('rival')===correctAnswers.rival) score++;

      // guardar en localStorage
      const saved = JSON.parse(localStorage.getItem('nacional_quiz')||'[]');
      saved.push({date:new Date().toISOString(),score, total});
      localStorage.setItem('nacional_quiz', JSON.stringify(saved));

      resultEl.style.display='block';
      resultEl.innerHTML = `<h3>Resultado: ${score} / ${total}</h3><p class="small">Se han guardado tus respuestas (localmente) — ${saved.length} intento(s) registrado(s).</p>`;
      this.reset();
    });

    /* ---------- TIMELINE: reveal on scroll ---------- */
    const events = document.querySelectorAll('.event');
    const observer = new IntersectionObserver((entries)=>{
      entries.forEach(entry=>{
        if(entry.isIntersecting){
          entry.target.classList.add('visible');
        }
      });
    },{threshold:0.15});
    events.forEach(ev=>observer.observe(ev));

    /* ------------------ SOPA DE LETRAS (mismo código) ------------------ */
    const ALL_WORD_POOLS = [
      ['NACIONAL','MEDELLIN','VERDOLAGA','HIGUITA','ARISTIZABAL','ATANASIO','GIRARDOT','ESCUDOS','MACNELLY','LIBERTADORES','HINCHADA','ATLETICO'],
      ['NACIONAL','VERDOLAGA','HIGUITA','ESCUDOR','ATANASIO','GIRARDOT','PLANTEL','COPA','MEDALLA','ARISTIZABAL'],
      ['ATLETICO','NACIONAL','MEDELLIN','HIGUITA','MACNELLY','ARISTIZABAL','GIRARDOT','LIBERTAD']
    ];

    const GRID_SIZE = 12; // NxN
    let grid = [];
    let placed = [];
    let selected = [];
    const gridEl = document.getElementById('grid');
    const wordListEl = document.getElementById('wordList');

    function randInt(n){ return Math.floor(Math.random()*n); }

    function pickWords(){
      const pool = ALL_WORD_POOLS[randInt(ALL_WORD_POOLS.length)];
      const shuffled = pool.slice().sort(()=>Math.random()-0.5);
      const count = Math.min(Math.max(6, Math.floor(Math.random()*3)+6), shuffled.length);
      return shuffled.slice(0,count).map(w=>w.toUpperCase());
    }

    function makeEmptyGrid(){
      grid = Array.from({length:GRID_SIZE}, ()=> Array.from({length:GRID_SIZE}, ()=> ''));
      placed = [];
    }

    const DIRS = [[1,0],[-1,0],[0,1],[0,-1],[1,1],[1,-1],[-1,1],[-1,-1]];

    function canPlace(word,x,y,dx,dy){
      for(let i=0;i<word.length;i++){
        const nx = x + dx*i; const ny = y + dy*i;
        if(nx<0||ny<0||nx>=GRID_SIZE||ny>=GRID_SIZE) return false;
        const c = grid[ny][nx];
        if(c!=='' && c!==word[i]) return false;
      }
      return true;
    }

    function placeWord(word){
      const attempts = 300;
      for(let a=0;a<attempts;a++){
        const dir = DIRS[randInt(DIRS.length)];
        const dx = dir[0], dy = dir[1];
        const x = randInt(GRID_SIZE); const y = randInt(GRID_SIZE);
        const endX = x + dx*(word.length-1); const endY = y + dy*(word.length-1);
        if(endX<0||endY<0||endX>=GRID_SIZE||endY>=GRID_SIZE) continue;
        if(canPlace(word,x,y,dx,dy)){
          const positions = [];
          for(let i=0;i<word.length;i++){
            const nx = x + dx*i; const ny = y + dy*i;
            grid[ny][nx] = word[i];
            positions.push([nx,ny]);
          }
          placed.push({word,positions,found:false});
          return true;
        }
      }
      return false;
    }

    function fillRandom(){
      const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
      for(let y=0;y<GRID_SIZE;y++){
        for(let x=0;x<GRID_SIZE;x++){
          if(grid[y][x]==='') grid[y][x]=letters[randInt(letters.length)];
        }
      }
    }

    function renderGrid(){
      gridEl.innerHTML='';
      for(let y=0;y<GRID_SIZE;y++){
        for(let x=0;x<GRID_SIZE;x++){
          const div = document.createElement('div');
          div.className = 'cell';
          div.dataset.x = x; div.dataset.y = y;
          div.textContent = grid[y][x];
          div.addEventListener('mousedown', startSel);
          div.addEventListener('mouseenter', overSel);
          div.addEventListener('mouseup', endSel);
          // touch
          div.addEventListener('touchstart', touchStart, {passive:false});
          div.addEventListener('touchmove', touchMove, {passive:false});
          div.addEventListener('touchend', endSel);
          gridEl.appendChild(div);
        }
      }
    }

    function renderWordList(){
      wordListEl.innerHTML='';
      placed.forEach(p=>{
        const span = document.createElement('div');
        span.className = 'word' + (p.found? ' found':'');
        span.textContent = p.word;
        span.dataset.word = p.word;
        wordListEl.appendChild(span);
      });
    }

    // Selection logic
    let mouseDown = false;
    let lastCell = null;

    function startSel(e){
      e.preventDefault();
      mouseDown = true;
      clearSelectionVisual();
      addCellSelection(e.currentTarget);
    }
    function overSel(e){
      if(!mouseDown) return;
      addCellSelection(e.currentTarget);
    }
    function endSel(e){
      if(!mouseDown) return;
      mouseDown = false;
      checkSelection();
    }

    function touchStart(e){
      e.preventDefault();
      const touch = e.touches[0];
      const el = document.elementFromPoint(touch.clientX, touch.clientY);
      if(el && el.classList.contains('cell')){
        mouseDown = true; clearSelectionVisual(); addCellSelection(el);
      }
    }
    function touchMove(e){
      e.preventDefault();
      const touch = e.touches[0];
      const el = document.elementFromPoint(touch.clientX, touch.clientY);
      if(el && el.classList.contains('cell')) addCellSelection(el);
    }

    function addCellSelection(el){
      if(!el) return;
      if(selected.length && selected[selected.length-1]===el) return;
      el.classList.add('sel');
      selected.push(el);
    }

    function clearSelectionVisual(){
      selected.forEach(c=>c.classList.remove('sel'));
      selected = [];
    }

    function checkSelection(){
      if(selected.length===0) return;
      const word = selected.map(c=>c.textContent).join('');
      const rev = selected.map(c=>c.textContent).reverse().join('');
      let matched = null;
      for(const p of placed){
        if(!p.found && (p.word === word || p.word === rev)){
          matched = p; break;
        }
      }
      if(matched){
        matched.found = true;
        for(const pos of matched.positions){
          const idx = pos[1]*GRID_SIZE + pos[0];
          const cell = gridEl.children[idx];
          if(cell){ cell.classList.remove('sel'); cell.classList.add('found'); }
        }
        renderWordList();
        checkWin();
      } else {
        selected.forEach(c=>{ c.style.transform='scale(0.95)'; setTimeout(()=>c.style.transform='scale(1)',180); });
      }
      selected = [];
    }

    function checkWin(){
      if(placed.every(p=>p.found)) setTimeout(()=>alert('¡Felicidades! Encontraste todas las palabras. 💚⚽'),60);
    }

    function showSolution(){
      placed.forEach(p=>{
        p.found = true;
        for(const pos of p.positions){
          const idx = pos[1]*GRID_SIZE + pos[0];
          const cell = gridEl.children[idx];
          if(cell) cell.classList.add('found');
        }
      });
      renderWordList();
    }

    function generateSopa(){
      makeEmptyGrid();
      const words = pickWords();
      words.sort((a,b)=>b.length-a.length);
      for(const w of words){ placeWord(w); }
      fillRandom();
      renderGrid();
      renderWordList();
    }

    async function recreateWithFade(){
      const card = document.querySelector('#sopa .card') || document.querySelector('.card');
      card.style.transition = 'opacity .28s';
      card.style.opacity = '0.25';
      await new Promise(r=>setTimeout(r,260));
      generateSopa();
      card.style.opacity = '1';
    }

    function clearSelection(){ clearSelectionVisual(); }

    document.getElementById('recrear').addEventListener('click', recreateWithFade);
    document.getElementById('mostrar').addEventListener('click', showSolution);
   document.getElementById('limpiar-seleccion').addEventListener('click', clearSelection);
    window.addEventListener('mouseup', ()=>{ if(mouseDown){ mouseDown=false; checkSelection(); } });

    // init
    generateSopa();

  </script>
</body>
</html>
