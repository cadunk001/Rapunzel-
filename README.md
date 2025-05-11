<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Uma Surpresa para Você</title>
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;700&display=swap" rel="stylesheet">
  <style>
    body {
      margin: 0;
      font-family: 'Dancing Script', cursive;
      background-color: #ffe6e6;
      color: #333;
      text-align: center;
      overflow-x: hidden;
    }
    header {
      padding: 50px;
      background: linear-gradient(to bottom, #ff9999, #ffe6e6);
    }
    h1 {
      font-size: 3em;
      color: #ff4d4d;
      text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
    }
    p {
      font-size: 1.5em;
      margin: 20px auto;
      max-width: 600px;
      line-height: 1.6;
    }
    .upload-section {
      margin: 20px auto;
      padding: 20px;
      background-color: #fff;
      border-radius: 10px;
      max-width: 600px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }
    input[type="file"] {
      margin: 10px;
      font-size: 1em;
    }
    .gallery {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 20px;
      padding: 20px;
    }
    .gallery img {
      max-width: 300px;
      border-radius: 15px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      transition: transform 0.3s;
    }
    .gallery img:hover {
      transform: scale(1.05);
    }
    .proposal {
      margin: 40px auto;
      padding: 20px;
      background-color: #fff;
      border-radius: 10px;
      max-width: 600px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }
    button {
      padding: 15px 30px;
      font-size: 1.2em;
      font-family: 'Dancing Script', cursive;
      background-color: #ff4d4d;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #e63939;
    }
    #proposal-text {
      display: none;
      font-size: 2em;
      color: #ff4d4d;
      margin-top: 20px;
      animation: fadeIn 2s;
    }
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
    audio {
      margin: 20px auto;
      display: block;
    }
    @media (max-width: 600px) {
      h1 { font-size: 2em; }
      p { font-size: 1.2em; }
      .gallery img { max-width: 100%; }
    }
  </style>
</head>
<body>
  <header>
    <h1>Para [Nome da Pessoa]</h1>
    <p>Você trouxe luz para minha vida, e quero te mostrar o quanto você é especial.</p>
  </header>

  <section class="upload-section">
    <h2>Adicione Nossas Fotos</h2>
    <input type="file" id="photoInput" accept="image/*" multiple>
    <button onclick="uploadPhotos()">Enviar Fotos</button>
  </section>

  <section class="gallery" id="gallery">
    <!-- Fotos serão adicionadas aqui dinamicamente -->
  </section>

  <section class="proposal">
    <p>Desde que te conheci, cada dia ficou mais colorido. Você é meu sorriso, meu conforto, meu tudo.</p>
    <button onclick="showProposal()">Tenho uma pergunta para você...</button>
    <div id="proposal-text">Quer ser minha namorada?</div>
  </section>

  <!-- Música de fundo opcional -->
  <audio controls autoplay loop>
    <source src="https://www.bensound.com/bensound-music/bensound-sweet.mp3" type="audio/mp3">
    Seu navegador não suporta áudio.
  </audio>

  <script>
    // Função para mostrar o pedido
    function showProposal() {
      const proposalText = document.getElementById('proposal-text');
      proposalText.style.display = 'block';
    }

    // Função para carregar fotos do LocalStorage
    function loadPhotos() {
      const gallery = document.getElementById('gallery');
      const savedPhotos = JSON.parse(localStorage.getItem('photos')) || [];
      gallery.innerHTML = '';
      savedPhotos.forEach(photo => {
        const img = document.createElement('img');
        img.src = photo;
        gallery.appendChild(img);
      });
    }

    // Função para fazer upload de fotos
    function uploadPhotos() {
      const photoInput = document.getElementById('photoInput');
      const files = photoInput.files;
      const savedPhotos = JSON.parse(localStorage.getItem('photos')) || [];

      for (let i = 0; i < files.length; i++) {
        const file = files[i];
        if (file.type.startsWith('image/')) {
          const reader = new FileReader();
          reader.onload = function(e) {
            savedPhotos.push(e.target.result);
            localStorage.setItem('photos', JSON.stringify(savedPhotos));
            loadPhotos();
          };
          reader.readAsDataURL(file);
        }
      }
    }

    // Carregar fotos ao abrir o site
    window.onload = loadPhotos;
  </script>
</body>
</html>
