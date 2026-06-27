<html lang="de-CH">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>KBL Bookspots</title>

  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800&display=swap" rel="stylesheet">

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Nunito', sans-serif;
      background: #101014;
      overflow-x: hidden;
      color: white;
    }

    .page {
      position: relative;
      width: 100%;
      min-height: 100vh;
      overflow: hidden;
    }

    .hero-title {
      position: absolute;
      top: 18px;
      left: 50%;
      transform: translateX(-50%);
      z-index: 10;

      background: rgba(0,0,0,0.45);
      backdrop-filter: blur(8px);

      padding: 12px 20px;
      border-radius: 18px;

      text-align: center;
      width: calc(100% - 32px);
      max-width: 500px;

      border: 1px solid rgba(255,255,255,0.1);
    }

    .hero-title h1 {
      font-size: 1.7rem;
      font-weight: 800;
      letter-spacing: 0.5px;
    }

    .hero-title p {
      margin-top: 4px;
      font-size: 0.92rem;
      opacity: 0.8;
    }

    .bookshelf {
      width: 100%;
      height: 100vh;
      object-fit: cover;
      display: block;
    }

    .star {
      position: absolute;
      width: 28px;
      height: 28px;
      border-radius: 50%;

      background:
        radial-gradient(circle,
        rgba(255,255,255,1) 0%,
        rgba(255,231,120,1) 35%,
        rgba(255,184,77,0.9) 60%,
        rgba(255,184,77,0) 100%);

      cursor: pointer;

      animation: pulse 2.8s infinite;

      box-shadow:
        0 0 8px rgba(255,200,80,0.8),
        0 0 20px rgba(255,200,80,0.4);

      transition: transform 0.2s ease;
    }

    .star::after {
      content: '✦';
      position: absolute;
      inset: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 16px;
      color: white;
    }

    .star:hover {
      transform: scale(1.1);
    }

    @keyframes pulse {
      0% {
        transform: scale(1);
        opacity: 0.9;
      }

      50% {
        transform: scale(1.15);
        opacity: 1;
      }

      100% {
        transform: scale(1);
        opacity: 0.9;
      }
    }

    .overlay {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.55);
      backdrop-filter: blur(5px);

      display: none;
      align-items: center;
      justify-content: center;

      z-index: 100;
      padding: 18px;
    }

    .overlay.active {
      display: flex;
    }

    .popup {
      position: relative;

      width: 100%;
      max-width: 360px;

      background: rgba(25,25,32,0.97);

      border-radius: 24px;
      overflow: hidden;

      border: 1px solid rgba(255,255,255,0.08);

      box-shadow:
        0 20px 40px rgba(0,0,0,0.45);

      animation: popupIn 0.2s ease;
    }

    .close-button {
        position: absolute;
        top: 12px;
        right: 12px;

        width: 36px;
        height: 36px;

        border: none;
        border-radius: 50%;

        background: rgba(0,0,0,0.45);
        backdrop-filter: blur(4px);

        color: white;
        font-size: 1rem;
        font-weight: bold;

        cursor: pointer;

        z-index: 20;

        transition:
            background 0.2s ease,
            transform 0.2s ease;
        }

        .close-button:hover {
        background: rgba(0,0,0,0.65);
        transform: scale(1.08);
        }

    @keyframes popupIn {
      from {
        opacity: 0;
        transform: scale(0.95);
      }

      to {
        opacity: 1;
        transform: scale(1);
      }
    }

    .popup img {
      width: 100%;
      height: 220px;
      object-fit: cover;
      display: block;
    }

    .popup-content {
      padding: 18px;
    }

    .popup-content h2 {
      font-size: 1.4rem;
      line-height: 1.2;
      margin-bottom: 6px;
    }

    .author {
      opacity: 0.7;
      margin-bottom: 14px;
      font-size: 0.95rem;
    }

    .signature {
      display: inline-block;
      margin-bottom: 14px;
      padding: 6px 10px;

      border-radius: 999px;
      background: rgba(255,255,255,0.08);

      font-size: 0.82rem;
      font-weight: 700;
    }

    .description {
      line-height: 1.45;
      font-size: 0.96rem;
      opacity: 0.92;
      margin-bottom: 18px;
    }

    .rating-section {
      margin-bottom: 18px;
      padding: 14px;
      border-radius: 18px;
      background: rgba(255,255,255,0.05);
    }

    .rating-title {
      margin-bottom: 10px;
      font-weight: 700;
      font-size: 0.95rem;
    }

    .stars-rating {
      display: flex;
      gap: 8px;
      margin-bottom: 10px;
    }

    .rate-star {
      font-size: 1.5rem;
      cursor: pointer;
      transition: transform 0.15s ease;
      user-select: none;
    }

    .rate-star:hover {
      transform: scale(1.15);
    }

    .rating-info {
      font-size: 0.88rem;
      opacity: 0.75;
    }

    .catalog-link {
      display: block;
      text-align: center;

      text-decoration: none;
      color: white;

      padding: 14px;
      border-radius: 16px;

      background: linear-gradient(135deg, #ff9f43, #ffb347);

      font-weight: 800;

      transition: transform 0.2s ease;
    }

    .catalog-link:hover {
      transform: translateY(-2px);
    }

    .hint {
      position: absolute;
      bottom: 18px;
      left: 50%;
      transform: translateX(-50%);

      z-index: 5;

      background: rgba(0,0,0,0.45);
      backdrop-filter: blur(6px);

      padding: 10px 16px;
      border-radius: 999px;

      font-size: 0.9rem;
      opacity: 0.85;
    }

    @media (max-width: 480px) {
      .hero-title h1 {
        font-size: 1.45rem;
      }

      .popup img {
        height: 200px;
      }
    }
  </style>
</head>
<body>

  <div class="page">

    <div class="hero-title">
      <h1>Bookspots ✨</h1>
      <p>Wenn dir Gregs Tagebuch gefällt, probier das!</p>
    </div>

    <!-- Eigenes Regalbild hier ersetzen -->
    <img
      class="bookshelf"
      src="Witziges.jpg"
      alt="Bücherregal"
    />

    <!-- Sterne -->
<!-- Jule Bambule -->
    <div class="star"
         style="top: 30%; left: 1%;"
         onclick="openBook(0)"></div>
<!-- O.M.G. Billie -->
    <div class="star"
         style="top: 29%; left: 20%;"
         onclick="openBook(1)"></div>
<!-- DORK Diaries -->
    <div class="star"
         style="top: 52%; left: 2.5%;"
         onclick="openBook(2)"></div>
<!-- Penny Pepper -->
    <div class="star"
         style="top: 50%; left: 70%;"
         onclick="openBook(3)"></div>
<!-- Lotta-Leben -->
    <div class="star"
         style="top: 32%; left: 90%;"
         onclick="openBook(4)"></div>
<!-- Tom Gates -->
    <div class="star"
         style="top: 70%; left: 90%;"
         onclick="openBook(5)"></div>
<!-- Super Nick -->
    <div class="star"
         style="top: 70%; left: 70%;"
         onclick="openBook(6)"></div>
<!-- Captain Underpants -->
    <div class="star"
         style="top: 32%; left: 25%;"
         onclick="openBook(7)"></div>
<!-- Worst Week -->
    <div class="star"
         style="top: 37%; left: 2.5%;"
         onclick="openBook(8)"></div>
<!-- Leon Mücke -->
    <div class="star"
         style="top: 88%; left: 15%;"
         onclick="openBook(9)"></div>


    <div class="hint">
      Tippe auf die leuchtenden Sterne ✨
    </div>

  </div>


  <!-- Popup -->

  <div class="overlay" id="overlay" onclick="closePopup(event)">

    <div class="popup" id="popup">

      <button
        class="close-button"
        onclick="manualClose(event)">
        ✕
      </button>

      <img id="popup-image" src="" alt="Buchcover">

      <div class="popup-content">

        <h2 id="popup-title"></h2>

        <div class="author" id="popup-author"></div>

        <div class="signature" id="popup-signature"></div>

        <div class="description" id="popup-description"></div>

        <div class="rating-section">
          <div class="rating-title">Wie fandest du das Buch?</div>

          <div class="stars-rating" id="stars-rating"></div>

          <div class="rating-info">
            <span id="average-rating">0.0</span> ★
            ·
            <span id="rating-count">0</span> Bewertungen
          </div>
        </div>

        <a
            class="catalog-link"
            id="popup-link"
            href="#"
            target="_blank"
            rel="noopener noreferrer"
            onclick="openCatalog(event)"
        >
          Im Katalog ansehen
        </a>

      </div>

    </div>

  </div>


  <script>

    const books = [
      {
        title: "Jule Bambule : Ente gut, alles gut",
        author: "Judith Allert",
        signature: "Jugend Witziges ALLE",
        lik: "LIK00461077X",
        location: "Witziges",
        description: "Jule stolpert von einem Chaos ins nächste – und genau das macht das Buch so lustig. Zwischen verrückten Ideen, peinlichen Situationen und tierischem Durcheinander wird es nie langweilig. Perfekt für Fans von witzigen Geschichten mit viel Tempo.",
        image: "Jule Bambule.jpg",
        link: "https://katalog.kbl.ch/results?p_r_p_arena_urn%3Aarena_search_item_id=61069ffc-a343-4ec1-afb4-41d0901589f1"
      },

      {
        title: "O.M.G. Billie! : Regel Nr. 1: Das Leben ist kein Kekskonzert",
        author: "Jen Carney",
        signature: "Jugend Witziges CARN",
        lik: "LIK004850291",
        location: "Witziges",
        description: "Billie versucht, das Chaos ihres Alltags zu überleben – was gar nicht so einfach ist. Schule, Familie und peinliche Situationen sorgen ständig für neue Katastrophen. Locker, modern und extrem lustig geschrieben.",
        image: "O.M.G. Billie.jpg",
        link: "https://katalog.kbl.ch/results?p_r_p_arena_urn%3Aarena_search_item_id=f48fbf55-3e5b-4b8e-9a8e-6cdd93558101"
      },

      {
        title: "Dork Diaries : Nikkis nicht ganz so fabelhafte Welt",
        author: "Rachel Renée Russell",
        signature: "Jugend Witziges DORK",
        lik: "LIK00422574X",
        location: "Witziges",
        description: "Nikki schreibt über ihren komplett verrückten Schulalltag. Zwischen Drama, Crushes und peinlichen Momenten entstehen superwitzige Tagebucheinträge mit vielen Zeichnungen. Ideal für Fans von Gregs Tagebuch.",
        image: "DORK Diaries.jpg",
        link: "https://katalog.kbl.ch/results?p_r_p_arena_urn%3Aarena_search_item_id=4bdf8ff1-4c80-4e5d-83b5-86404c2d4368"
      },

      {
        title: "Penny Pepper : Alles kein Problem!",
        author: "Ulrike Rylance",
        signature: "Jugend Witziges PENN",
        lik: "LIK004558497",
        location: "Witziges",
        description: "Penny liebt Detektivfälle und steckt ihre Nase überall hinein. Zusammen mit ihren Freunden löst sie spannende Rätsel und gerät dabei oft in Schwierigkeiten. Witzig, clever und voller Überraschungen.",
        image: "Penny Pepper.jpg",
        link: "https://katalog.kbl.ch/results?p_r_p_arena_urn%3Aarena_search_item_id=926f5b03-8d76-4c33-bbf4-2a0465048f96"
      },

      {
        title: "Mein Lotta-Leben : Alles voller Kaninchen",
        author: "Alice Pantermüller",
        signature: "Jugend Witziges MEIN",
        lik: "LIK004609951",
        location: "Witziges",
        description: "Lotta erzählt von ihrem total verrückten Alltag mit Familie, Schule und jeder Menge Missverständnissen. Die lustigen Zeichnungen machen das Lesen besonders leicht. Charmant, chaotisch und mega unterhaltsam.",
        image: "Lotta-Leben.jpg",
        link: "https://katalog.kbl.ch/results?p_r_p_arena_urn%3Aarena_search_item_id=f74e0edc-609e-4aba-b6f9-78aa616512a6"
      },

      {
        title: "Tom Gates : Wo ich bin, ist Chaos",
        author: "Liz Pichon",
        signature: "Jugend Witziges TOMG",
        lik: "LIK004007045",
        location: "Witziges",
        description: "Tom zeichnet lieber Comics, als Hausaufgaben zu machen. Sein Leben besteht aus Musik, Snacks und ziemlich viel Chaos. Die vielen Kritzeleien und Witze machen das Buch supercool.",
        image: "Tom Gates.jpg",
        link: "https://katalog.kbl.ch/results?p_r_p_arena_urn%3Aarena_search_item_id=ca05449f-5464-4834-9438-2ae2f9c1dc56"
      },

      {
        title: "Super Nick : Bis später, ihr Pfeifen!",
        author: "Lincoln Peirce",
        signature: "Jugend Witziges SUPE",
        lik: "LIK004704488",
        location: "Witziges",
        description: "Nick steckt dauernd in lustigen oder peinlichen Situationen. Schule, Freunde und Lehrer sorgen für nonstop Ärger und jede Menge Lacher. Comicstil und kurze Kapitel machen das Buch extrem angenehm zu lesen.",
        image: "Super Nick.jpg",
        link: "https://katalog.kbl.ch/results?p_r_p_arena_urn%3Aarena_search_item_id=53812431-1a2a-4e67-a525-4e218ca6c148"
      },

      {
        title: "Die Abenteuer des Captain Underpants",
        author: "Dav Pilkey",
        signature: "Jugend Witziges CAPT",
        lik: "LIK004829320",
        location: "Witziges",
        description: "Zwei Freunde verwandeln ihren strengen Direktor aus Versehen in einen Superhelden mit Unterhose und Umhang. Komplett verrückt, überdreht und voller Comic-Humor. Perfekt für alle, die absurde Geschichten lieben.",
        image: "Captain Underpants.jpg",
        link: "https://katalog.kbl.ch/results?p_r_p_arena_urn%3Aarena_search_item_id=72b55683-f5b8-4558-9c20-c61d44d57e4d"
      },

      {
        title: "Worst week ever! : Montag",
        author: "Eva Amores & Matt Cosgrove",
        signature: "Jugend Witziges AMOR",
        lik: "LIK004881151",
        location: "Witziges",
        description: "Schon am Montag läuft einfach alles schief. Von peinlichen Momenten bis zu total verrückten Katastrophen wird die Woche immer schlimmer. Schnell, witzig und voller Comiczeichnungen.",
        image: "Worst week ever.jpg",
        link: "https://katalog.kbl.ch/results?p_r_p_arena_urn%3Aarena_search_item_id=3602e40c-e80e-462b-8cb7-2b74ba97184f"
      },

      {
        title: "Leon Mücke : Kein Plan, aber für alles eine Lösung",
        author: "Jakob Musashi Leonhardt",
        signature: "Jugend Witziges LEON",
        lik: "LIK004984777",
        location: "Witziges",
        description: "Leon hat zwar selten einen Plan, aber irgendwie landet er trotzdem mitten im Abenteuer. Seine Ideen führen oft zu totalem Chaos – und genau das macht Spass. Locker geschrieben und perfekt für Wenigleser:innen.",
        image: "Leon Mücke.jpg",
        link: "https://katalog.kbl.ch/results?p_r_p_arena_urn%3Aarena_search_item_id=18213eaf-b0cc-4857-a2eb-e80ffb5f1601"
      }
    ];


    let currentBookIndex = 0;

    function getRatings(index) {
      const stored = localStorage.getItem(`ratings-${index}`);

      if (stored) {
        return JSON.parse(stored);
      }

      return [];
    }

    function saveRating(index, rating) {
      const ratings = getRatings(index);
      ratings.push(rating);
      localStorage.setItem(`ratings-${index}`, JSON.stringify(ratings));
    }

    function renderRating(index) {

      const starsContainer = document.getElementById('stars-rating');
      starsContainer.innerHTML = '';

      for (let i = 1; i <= 5; i++) {

        const star = document.createElement('span');
        star.className = 'rate-star';
        star.innerHTML = '⭐';

        star.onclick = () => {
          saveRating(index, i);
          renderRating(index);
        };

        starsContainer.appendChild(star);
      }

      const ratings = getRatings(index);

      const count = ratings.length;

      const average = count
        ? (ratings.reduce((a, b) => a + b, 0) / count).toFixed(1)
        : '0.0';

      document.getElementById('average-rating').innerText = average;
      document.getElementById('rating-count').innerText = count;
    }


    function openBook(index) {

      currentBookIndex = index;

      const book = books[index];

      document.getElementById('popup-title').innerText = book.title;
      document.getElementById('popup-author').innerText = book.author;
      document.getElementById('popup-signature').innerText = book.signature;
      document.getElementById('popup-description').innerText = book.description;
      document.getElementById('popup-image').src = book.image;
      document.getElementById('popup-link').href = book.link;

      renderRating(index);

      document.getElementById('overlay').classList.add('active');
    }


    function closePopup(event) {

        const popup = document.getElementById('popup');

        if (!popup.contains(event.target)) {
            document.getElementById('overlay').classList.remove('active');
        }
        }


        function manualClose(event) {

        if (event) {
            event.stopPropagation();
        }

        document.getElementById('overlay').classList.remove('active');
        }

    async function openCatalog(event) {

        event.preventDefault();

        const link = books[currentBookIndex].link;

        // Versuch: automatisch kopieren
        try {
            await navigator.clipboard.writeText(link);

            // Versuch: neuer Tab
            const newWindow = window.open(
            link,
            '_blank',
            'noopener,noreferrer'
            );

            // Falls Browser blockiert:
            if (!newWindow || newWindow.closed || typeof newWindow.closed === 'undefined') {

            alert(
                'Der Kataloglink wurde kopiert.\n\n' +
                'Falls sich nichts öffnet:\n' +
                'Neuen Tab öffnen → Link einfügen.'
            );
            }

        } catch (err) {

            // Fallback für ältere Browser
            const textArea = document.createElement('textarea');
            textArea.value = link;

            document.body.appendChild(textArea);

            textArea.select();
            document.execCommand('copy');

            document.body.removeChild(textArea);

            alert(
            'Der Kataloglink wurde kopiert.\n\n' +
            'Bitte in einem neuen Tab einfügen.'
            );
        }
    }
  </script>

</body>
</html>
