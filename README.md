# MorocoPlay
pagina para subir tus video juegos
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>GameHub - Tu Portal de Videojuegos</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style id="app-style">
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: #121826;
      color: #e4e6eb;
    }
    
    .nav-tab {
      position: relative;
      cursor: pointer;
      transition: all 0.3s ease;
    }
    
    .nav-tab.active {
      color: #38bdf8;
    }
    
    .nav-tab.active::after {
      content: '';
      position: absolute;
      bottom: -5px;
      left: 0;
      width: 100%;
      height: 3px;
      background-color: #38bdf8;
      border-radius: 2px;
    }
    
    .game-card {
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      cursor: pointer;
    }
    
    .game-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.3);
    }

    .tag {
      background: linear-gradient(135deg, #6366f1 0%, #4f46e5 100%);
    }
    
    .spinner {
      border: 4px solid rgba(0, 0, 0, 0.1);
      width: 36px;
      height: 36px;
      border-radius: 50%;
      border-left-color: #38bdf8;
      animation: spin 1s linear infinite;
    }
    
    @keyframes spin {
      0% {
        transform: rotate(0deg);
      }
      100% {
        transform: rotate(360deg);
      }
    }
    
    .ad-container {
      background: rgba(255, 255, 255, 0.05);
      border: 1px dashed rgba(255, 255, 255, 0.2);
    }
    
    .game-expanded {
      max-height: 800px;
      transition: max-height 0.5s ease-in-out;
    }
    
    .submit-button {
      background: linear-gradient(135deg, #3b82f6 0%, #2563eb 100%);
      transition: all 0.3s ease;
    }
    
    .submit-button:hover {
      background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
      transform: translateY(-2px);
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
    }
    
    .browse-container {
      min-height: 400px;
    }
    
    .tab-content {
      animation: fadeIn 0.5s ease-in-out;
    }
    
    @keyframes fadeIn {
      from {
        opacity: 0;
        transform: translateY(10px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .custom-scrollbar::-webkit-scrollbar {
      width: 6px;
    }
    
    .custom-scrollbar::-webkit-scrollbar-track {
      background: rgba(255, 255, 255, 0.05);
    }
    
    .custom-scrollbar::-webkit-scrollbar-thumb {
      background: rgba(255, 255, 255, 0.2);
      border-radius: 3px;
    }
  </style>
</head>

<body class="min-h-screen">
  <!-- Loading Spinner -->
  <div id="loading-spinner" class="fixed top-0 left-0 w-full h-full bg-black bg-opacity-70 flex items-center justify-center z-50 hidden">
    <div class="spinner"></div>
  </div>

  <!-- Header -->
  <header class="bg-gray-900 shadow-lg">
    <div class="container mx-auto px-4 py-4 flex flex-col md:flex-row justify-between items-center">
      <div class="flex items-center mb-4 md:mb-0">
        <i class="fas fa-gamepad text-3xl text-blue-500 mr-3"></i>
        <h1 class="text-2xl font-bold text-white">GameHub</h1>
      </div>
      
      <div class="flex space-x-8">
        <div id="tab-submit" class="nav-tab active text-lg font-medium py-2">
          <i class="fas fa-upload mr-2"></i>Subir Juego
        </div>
        <div id="tab-browse" class="nav-tab text-lg font-medium py-2">
          <i class="fas fa-search mr-2"></i>Explorar Juegos
        </div>
      </div>
    </div>
  </header>

  <!-- Main Content -->
  <main class="container mx-auto px-4 py-8">
    <!-- Top Ad Banner -->
    <div class="ad-container w-full h-24 mb-8 rounded-lg flex items-center justify-center">
      <p class="text-gray-400"><i class="fas fa-ad mr-2"></i> Espacio para anuncio de AdSense</p>
    </div>

    <div class="flex flex-col lg:flex-row gap-8">
      <!-- Main Content -->
      <div class="w-full lg:w-3/4">
        <!-- Submit Game Tab -->
        <div id="content-submit" class="tab-content">
          <div class="bg-gray-800 rounded-xl shadow-lg p-6">
            <h2 class="text-2xl font-bold mb-6 text-blue-400">Sube tu Videojuego</h2>
            
            <form id="game-submit-form" class="space-y-6">
              <div>
                <label class="block text-sm font-medium mb-2">Título del juego</label>
                <input type="text" id="game-title" class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 focus:border-blue-500 focus:ring focus:ring-blue-500 focus:ring-opacity-50 outline-none transition" placeholder="Ingresa el título de tu juego">
                <p class="validation-message hidden text-red-500 text-sm mt-1"></p>
              </div>
              
              <div>
                <label class="block text-sm font-medium mb-2">Descripción</label>
                <textarea id="game-description" rows="4" class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 focus:border-blue-500 focus:ring focus:ring-blue-500 focus:ring-opacity-50 outline-none transition custom-scrollbar" placeholder="Describe tu juego aquí..."></textarea>
                <p class="validation-message hidden text-red-500 text-sm mt-1"></p>
              </div>
              
              <div>
                <label class="block text-sm font-medium mb-2">URL de la imagen de portada</label>
                <input type="text" id="game-thumbnail" class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 focus:border-blue-500 focus:ring focus:ring-blue-500 focus:ring-opacity-50 outline-none transition" placeholder="https://ejemplo.com/imagen.jpg">
                <p class="validation-message hidden text-red-500 text-sm mt-1"></p>
              </div>
              
              <div>
                <label class="block text-sm font-medium mb-2">URL para incrustar el juego</label>
                <input type="text" id="game-embed" class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 focus:border-blue-500 focus:ring focus:ring-blue-500 focus:ring-opacity-50 outline-none transition" placeholder="https://ejemplo.com/juego.html">
                <p class="validation-message hidden text-red-500 text-sm mt-1"></p>
              </div>
              
              <div>
                <label class="block text-sm font-medium mb-2">Etiquetas (separadas por comas)</label>
                <input type="text" id="game-tags" class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 focus:border-blue-500 focus:ring focus:ring-blue-500 focus:ring-opacity-50 outline-none transition" placeholder="acción, aventura, puzzle">
              </div>
              
              <div class="flex justify-end">
                <button type="submit" class="submit-button px-6 py-3 rounded-lg text-white font-medium">
                  <i class="fas fa-paper-plane mr-2"></i>Publicar Juego
                </button>
              </div>
            </form>
          </div>
          
          <!-- Preview Section -->
          <div class="mt-8 bg-gray-800 rounded-xl shadow-lg p-6">
            <h3 class="text-xl font-bold mb-4 text-blue-400">Vista Previa</h3>
            
            <div id="preview-container" class="bg-gray-900 rounded-lg p-4 flex flex-col items-center">
              <p id="no-preview" class="text-gray-400 py-12"><i class="fas fa-eye-slash mr-2"></i> Completa el formulario para ver la vista previa</p>
              
              <div id="preview-content" class="hidden w-full">
                <div class="mb-4 w-full">
                  <img id="preview-thumbnail" src="" alt="Game Thumbnail" class="w-full h-48 object-cover rounded-lg mb-3">
                  <h4 id="preview-title" class="text-lg font-bold"></h4>
                  <p id="preview-description" class="text-gray-300 text-sm mt-2"></p>
                  <div id="preview-tags" class="flex flex-wrap gap-2 mt-3"></div>
                </div>
                
                <div class="mt-6 w-full">
                  <h5 class="text-sm font-medium mb-2 text-gray-400">Vista previa del juego:</h5>
                  <div id="preview-embed" class="w-full h-80 bg-black rounded-lg flex items-center justify-center">
                    <p class="text-gray-500"><i class="fas fa-gamepad mr-2"></i> El juego se mostrará aquí</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Browse Games Tab -->
        <div id="content-browse" class="tab-content hidden">
          <div class="bg-gray-800 rounded-xl shadow-lg p-6 mb-8">
            <div class="flex flex-col md:flex-row gap-4 mb-6">
              <div class="relative flex-grow">
                <input type="text" id="search-games" class="w-full pl-10 pr-4 py-2 rounded-md bg-gray-700 border border-gray-600 focus:border-blue-500 focus:ring focus:ring-blue-500 focus:ring-opacity-50 outline-none transition" placeholder="Buscar juegos...">
                <i class="fas fa-search absolute left-3 top-3 text-gray-400"></i>
              </div>
              
              <select id="filter-tags" class="px-4 py-2 rounded-md bg-gray-700 border border-gray-600 focus:border-blue-500 focus:ring focus:ring-blue-500 focus:ring-opacity-50 outline-none transition">
                <option value="">Todas las etiquetas</option>
                <option value="acción">Acción</option>
                <option value="aventura">Aventura</option>
                <option value="puzzle">Puzzle</option>
                <option value="rpg">RPG</option>
                <option value="estrategia">Estrategia</option>
              </select>
            </div>

            <div class="browse-container">
              <div id="games-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Games will be loaded here -->
                <p class="text-gray-400 col-span-full text-center py-12">Cargando juegos...</p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Sidebar -->
      <div class="w-full lg:w-1/4">
        <!-- Sidebar Ad Container -->
        <div class="ad-container h-96 rounded-lg flex items-center justify-center mb-6">
          <p class="text-gray-400"><i class="fas fa-ad mr-2"></i> Anuncio Lateral</p>
        </div>
        
        <!-- Featured Games -->
        <div class="bg-gray-800 rounded-xl shadow-lg p-4 mb-6">
          <h3 class="text-xl font-bold mb-4 text-blue-400">Juegos Destacados</h3>
          <div class="space-y-4">
            <div class="flex gap-3">
              <img src="https://cdn.pixabay.com/photo/2021/09/07/07/11/game-console-6603120_960_720.jpg" alt="Featured Game" class="w-20 h-20 rounded object-cover">
              <div>
                <h4 class="font-medium">Cosmic Adventure</h4>
                <p class="text-xs text-gray-400">Explora galaxias lejanas</p>
                <div class="flex gap-1 mt-1">
                  <span class="text-xs px-2 py-1 bg-blue-600 bg-opacity-30 rounded-full">Espacio</span>
                  <span class="text-xs px-2 py-1 bg-blue-600 bg-opacity-30 rounded-full">Aventura</span>
                </div>
              </div>
            </div>
            
            <div class="flex gap-3">
              <img src="https://cdn.pixabay.com/photo/2016/10/30/23/05/controller-1784573_960_720.jpg" alt="Featured Game" class="w-20 h-20 rounded object-cover">
              <div>
                <h4 class="font-medium">Ninja Warrior</h4>
                <p class="text-xs text-gray-400">Batalla épica de ninjas</p>
                <div class="flex gap-1 mt-1">
                  <span class="text-xs px-2 py-1 bg-blue-600 bg-opacity-30 rounded-full">Acción</span>
                  <span class="text-xs px-2 py-1 bg-blue-600 bg-opacity-30 rounded-full">Lucha</span>
                </div>
              </div>
            </div>
            
            <div class="flex gap-3">
              <img src="https://cdn.pixabay.com/photo/2019/12/04/11/37/game-4672296_960_720.png" alt="Featured Game" class="w-20 h-20 rounded object-cover">
              <div>
                <h4 class="font-medium">Puzzle Master</h4>
                <p class="text-xs text-gray-400">Desafía tu mente</p>
                <div class="flex gap-1 mt-1">
                  <span class="text-xs px-2 py-1 bg-blue-600 bg-opacity-30 rounded-full">Puzzle</span>
                  <span class="text-xs px-2 py-1 bg-blue-600 bg-opacity-30 rounded-full">Estrategia</span>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Tips for Developers -->
        <div class="bg-gray-800 rounded-xl shadow-lg p-4">
          <h3 class="text-xl font-bold mb-4 text-blue-400">Consejos para Desarrolladores</h3>
          <ul class="space-y-2 text-sm">
            <li class="flex gap-2">
              <i class="fas fa-check-circle text-green-400 mt-1"></i>
              <span>Asegúrate de que tu juego sea compatible con múltiples dispositivos</span>
            </li>
            <li class="flex gap-2">
              <i class="fas fa-check-circle text-green-400 mt-1"></i>
              <span>Usa etiquetas relevantes para aumentar la visibilidad</span>
            </li>
            <li class="flex gap-2">
              <i class="fas fa-check-circle text-green-400 mt-1"></i>
              <span>Proporciona una descripción detallada de tu juego</span>
            </li>
            <li class="flex gap-2">
              <i class="fas fa-check-circle text-green-400 mt-1"></i>
              <span>Usa imágenes de alta calidad para la portada</span>
            </li>
            <li class="flex gap-2">
              <i class="fas fa-check-circle text-green-400 mt-1"></i>
              <span>Actualiza tu juego regularmente para mantener a los jugadores interesados</span>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </main>

  <!-- Footer -->
  <footer class="bg-gray-900 py-6 mt-12">
    <div class="container mx-auto px-4">
      <div class="flex flex-col md:flex-row justify-between items-center">
        <div class="mb-4 md:mb-0">
          <div class="flex items-center">
            <i class="fas fa-gamepad text-2xl text-blue-500 mr-2"></i>
            <h2 class="text-xl font-bold">GameHub</h2>
          </div>
          <p class="text-sm text-gray-400 mt-1">Tu portal para compartir y descubrir videojuegos</p>
        </div>
        
        <div class="flex space-x-4">
          <a href="javascript:void(0)" class="text-gray-400 hover:text-white transition">
            <i class="fab fa-twitter text-xl"></i>
          </a>
          <a href="javascript:void(0)" class="text-gray-400 hover:text-white transition">
            <i class="fab fa-facebook text-xl"></i>
          </a>
          <a href="javascript:void(0)" class="text-gray-400 hover:text-white transition">
            <i class="fab fa-instagram text-xl"></i>
          </a>
          <a href="javascript:void(0)" class="text-gray-400 hover:text-white transition">
            <i class="fab fa-discord text-xl"></i>
          </a>
        </div>
      </div>
      
      <div class="border-t border-gray-800 my-6"></div>
      
      <div class="flex flex-col md:flex-row justify-between items-center">
        <p class="text-sm text-gray-500">© 2025 GameHub. Todos los derechos reservados.</p>
        
        <div class="flex space-x-6 mt-4 md:mt-0">
          <a href="javascript:void(0)" class="text-sm text-gray-500 hover:text-gray-300 transition">Términos de Uso</a>
          <a href="javascript:void(0)" class="text-sm text-gray-500 hover:text-gray-300 transition">Política de Privacidad</a>
          <a href="javascript:void(0)" class="text-sm text-gray-500 hover:text-gray-300 transition">Contacto</a>
        </div>
      </div>
    </div>
  </footer>

  <script id="app-script">
    // Tab navigation
    $(document).ready(function() {
      // Tab switching functionality
      $('#tab-submit').click(function() {
        $('.nav-tab').removeClass('active');
        $(this).addClass('active');
        $('.tab-content').addClass('hidden');
        $('#content-submit').removeClass('hidden');
      });
      
      $('#tab-browse').click(function() {
        $('.nav-tab').removeClass('active');
        $(this).addClass('active');
        $('.tab-content').addClass('hidden');
        $('#content-browse').removeClass('hidden');
        
        // Load games when browse tab is opened
        loadGames();
      });
      
      // Form preview functionality
      $('#game-title, #game-description, #game-thumbnail, #game-embed, #game-tags').on('input', function() {
        updatePreview();
      });
      
      // Form submission
      $('#game-submit-form').submit(function(e) {
        e.preventDefault();
        
        // Show loading spinner
        $('#loading-spinner').removeClass('hidden');
        
        // Validate form
        let isValid = true;
        
        const title = $('#game-title').val().trim();
        const description = $('#game-description').val().trim();
        const thumbnail = $('#game-thumbnail').val().trim();
        const embed = $('#game-embed').val().trim();
        
        if (!title) {
          showValidationError($('#game-title'), 'El título es obligatorio');
          isValid = false;
        } else {
          hideValidationError($('#game-title'));
        }
        
        if (!description) {
          showValidationError($('#game-description'), 'La descripción es obligatoria');
          isValid = false;
        } else {
          hideValidationError($('#game-description'));
        }
        
        if (!thumbnail) {
          showValidationError($('#game-thumbnail'), 'La URL de la imagen es obligatoria');
          isValid = false;
        } else if (!isValidUrl(thumbnail)) {
          showValidationError($('#game-thumbnail'), 'Ingresa una URL válida');
          isValid = false;
        } else {
          hideValidationError($('#game-thumbnail'));
        }
        
        if (!embed) {
          showValidationError($('#game-embed'), 'La URL para incrustar el juego es obligatoria');
          isValid = false;
        } else if (!isValidUrl(embed)) {
          showValidationError($('#game-embed'), 'Ingresa una URL válida');
          isValid = false;
        } else {
          hideValidationError($('#game-embed'));
        }
        
        // Submit if valid
        if (isValid) {
          // Simulate API call
          setTimeout(function() {
            // Clear form
            $('#game-submit-form')[0].reset();
            $('#preview-content').addClass('hidden');
            $('#no-preview').removeClass('hidden');
            
            // Show success message
            alert('¡Juego publicado con éxito!');
            
            // Hide loading spinner
            $('#loading-spinner').addClass('hidden');
            
            // Switch to browse tab
            $('#tab-browse').click();
          }, 1500);
        } else {
          $('#loading-spinner').addClass('hidden');
        }
      });
      
      // Load initial games
      loadGames();
    });
    
    function updatePreview() {
      const title = $('#game-title').val().trim();
      const description = $('#game-description').val().trim();
      const thumbnail = $('#game-thumbnail').val().trim();
      const embed = $('#game-embed').val().trim();
      const tags = $('#game-tags').val().trim();
      
      if (title || description || thumbnail || embed) {
        $('#no-preview').addClass('hidden');
        $('#preview-content').removeClass('hidden');
        
        $('#preview-title').text(title || 'Sin título');
        $('#preview-description').text(description || 'Sin descripción');
        
        if (thumbnail && isValidUrl(thumbnail)) {
          $('#preview-thumbnail').attr('src', thumbnail);
        } else {
          $('#preview-thumbnail').attr('src', 'https://cdn.pixabay.com/photo/2016/10/30/23/05/controller-1784573_960_720.jpg');
        }
        
        // Update tags
        $('#preview-tags').empty();
        if (tags) {
          const tagArray = tags.split(',');
          tagArray.forEach(function(tag) {
            if (tag.trim()) {
              $('#preview-tags').append(`<span class="tag text-xs px-2 py-1 rounded-full text-white">${tag.trim()}</span>`);
            }
          });
        }
        
        // Update embed
        if (embed && isValidUrl(embed)) {
          $('#preview-embed').html(`<iframe src="${embed}" class="w-full h-full rounded-lg"></iframe>`);
        } else {
          $('#preview-embed').html('<p class="text-gray-500"><i class="fas fa-gamepad mr-2"></i> Ingresa una URL válida para ver el juego</p>');
        }
      } else {
        $('#preview-content').addClass('hidden');
        $('#no-preview').removeClass('hidden');
      }
    }
    
    function isValidUrl(url) {
      try {
        new URL(url);
        return true;
      } catch (e) {
        return false;
      }
    }
    
    function showValidationError(element, message) {
      const errorElement = element.next('.validation-message');
      errorElement.text(message);
      errorElement.removeClass('hidden');
      element.addClass('border-red-500');
    }
    
    function hideValidationError(element) {
      const errorElement = element.next('.validation-message');
      errorElement.addClass('hidden');
      element.removeClass('border-red-500');
    }
    
    function loadGames() {
      $('#loading-spinner').removeClass('hidden');
      
      // Simulate API call to get games
      setTimeout(function() {
        // Sample games data
        const games = [
          {
            id: 1,
            title: 'Space Explorer',
            description: 'Explora el vasto universo en esta aventura épica. Descubre nuevos planetas y combate alienígenas hostiles mientras navegas a través de galaxias desconocidas.',
            thumbnail: 'https://cdn.pixabay.com/photo/2020/09/03/15/30/spacecraft-5541538_960_720.jpg',
            embed: 'https://example.com/space-explorer',
            tags: ['aventura', 'espacio', 'acción']
          },
          {
            id: 2,
            title: 'Monster Hunter',
            description: 'Caza monstruos legendarios en un mundo abierto lleno de peligros y tesoros ocultos. Mejora tus armas y equipo para enfrentarte a bestias cada vez más fuertes.',
            thumbnail: 'https://cdn.pixabay.com/photo/2018/09/16/22/08/fantasy-3682178_960_720.jpg',
            embed: 'https://example.com/monster-hunter',
            tags: ['rpg', 'aventura', 'acción']
          },
          {
            id: 3,
            title: 'Puzzle Master',
            description: 'Pon a prueba tu ingenio con cientos de acertijos que desafiarán tu mente. Desde simples rompecabezas hasta complejos enigmas lógicos.',
            thumbnail: 'https://cdn.pixabay.com/photo/2017/08/14/05/42/people-2639398_960_720.jpg',
            embed: 'https://example.com/puzzle-master',
            tags: ['puzzle', 'lógica', 'casual']
          },
          {
            id: 4,
            title: 'Racing Championship',
            description: 'Compite en carreras de alta velocidad en pistas de todo el mundo. Personaliza tu vehículo y supera a tus oponentes para convertirte en el campeón mundial.',
            thumbnail: 'https://cdn.pixabay.com/photo/2016/11/18/12/14/car-1834373_960_720.jpg',
            embed: 'https://example.com/racing-championship',
            tags: ['carreras', 'deportes', 'simulación']
          },
          {
            id: 5,
            title: 'Zombie Survival',
            description: 'Sobrevive al apocalipsis zombie en este intenso juego de supervivencia. Construye refugios, busca suministros y defiéndete de hordas de no-muertos.',
            thumbnail: 'https://cdn.pixabay.com/photo/2018/03/06/06/58/horror-3202707_960_720.jpg',
            embed: 'https://example.com/zombie-survival',
            tags: ['supervivencia', 'horror', 'acción']
          },
          {
            id: 6,
            title: 'Strategy Empire',
            description: 'Construye y expande tu imperio en este juego de estrategia por turnos. Gestiona recursos, forma alianzas y conquista territorios enemigos.',
            thumbnail: 'https://cdn.pixabay.com/photo/2016/12/02/02/10/idea-1876659_960_720.jpg',
            embed: 'https://example.com/strategy-empire',
            tags: ['estrategia', 'por turnos', 'histórico']
          }
        ];
        
        renderGames(games);
        $('#loading-spinner').addClass('hidden');
      }, 1000);
    }
    
    function renderGames(games) {
      const gamesGrid = $('#games-grid');
      gamesGrid.empty();
      
      if (games.length === 0) {
        gamesGrid.html('<p class="text-gray-400 col-span-full text-center py-12">No se encontraron juegos</p>');
        return;
      }
      
      games.forEach(function(game, index) {
        // Add game card
        const gameCard = $(`
          <div class="game-card bg-gray-700 rounded-lg overflow-hidden shadow-lg">
            <div class="relative">
              <img src="${game.thumbnail}" alt="${game.title}" class="w-full h-48 object-cover">
              <div class="absolute top-2 right-2 bg-blue-600 text-white text-xs px-2 py-1 rounded-full">
                ${game.tags[0] || 'Juego'}
              </div>
            </div>
            <div class="p-4">
              <h3 class="font-bold text-lg mb-1">${game.title}</h3>
              <p class="text-gray-300 text-sm h-12 overflow-hidden">${game.description.substring(0, 100)}${game.description.length > 100 ? '...' : ''}</p>
              
              <div class="flex flex-wrap gap-1 mt-3">
                ${game.tags.map(tag => `<span class="tag text-xs px-2 py-1 rounded-full text-white">${tag}</span>`).join('')}
              </div>
              
              <button class="play-button w-full mt-4 bg-blue-600 hover:bg-blue-700 text-white py-2 rounded-md transition" data-id="${game.id}">
                <i class="fas fa-play mr-2"></i>Jugar Ahora
              </button>
            </div>
            <div class="game-embed-container h-0 overflow-hidden transition-all duration-500"></div>
          </div>
        `);
        
        gamesGrid.append(gameCard);
        
        // Insert ad after every 3 games
        if ((index + 1) % 3 === 0 && index < games.length - 1) {
          const adElement = $(`
            <div class="col-span-1 md:col-span-2 lg:col-span-3 ad-container h-24 rounded-lg flex items-center justify-center">
              <p class="text-gray-400"><i class="fas fa-ad mr-2"></i> Anuncio</p>
            </div>
          `);
          gamesGrid.append(adElement);
        }
      });
      
      // Add play button functionality
      $('.play-button').click(function() {
        const gameId = $(this).data('id');
        const card = $(this).closest('.game-card');
        const embedContainer = card.find('.game-embed-container');
        
        if (embedContainer.height() === 0) {
          // Show loading spinner
          $('#loading-spinner').removeClass('hidden');
          
          // Close any open game containers
          $('.game-embed-container').height(0);
          $('.play-button').html('<i class="fas fa-play mr-2"></i>Jugar Ahora');
          
          // Change button text
          $(this).html('<i class="fas fa-times mr-2"></i>Cerrar Juego');
          
          // Get game data
          const game = games.find(g => g.id === gameId);
          
          // Simulate loading game
          setTimeout(function() {
            // Add iframe to container
            embedContainer.html(`
              <div class="p-4">
                <div class="bg-black rounded-lg">
                  <iframe src="about:blank" class="w-full h-80 rounded-lg" title="${game.title}"></iframe>
                  <div class="bg-gray-800 p-3 text-center">
                    <p class="text-sm">Esta es una versión prototipo. El juego real se cargará en la versión completa.</p>
                  </div>
                </div>
              </div>
            `);
            
            // Expand container
            embedContainer.height('auto');
            
            // Hide loading spinner
            $('#loading-spinner').addClass('hidden');
          }, 1500);
        } else {
          // Change button text back
          $(this).html('<i class="fas fa-play mr-2"></i>Jugar Ahora');
          
          // Collapse container
          embedContainer.height(0);
          
          // Clear content after transition
          setTimeout(function() {
            embedContainer.empty();
          }, 500);
        }
      });
      
      // Add search functionality
      $('#search-games').on('input', function() {
        const searchTerm = $(this).val().toLowerCase();
        const filterTag = $('#filter-tags').val().toLowerCase();
        
        filterGames(games, searchTerm, filterTag);
      });
      
      // Add filter functionality
      $('#filter-tags').change(function() {
        const filterTag = $(this).val().toLowerCase();
        const searchTerm = $('#search-games').val().toLowerCase();
        
        filterGames(games, searchTerm, filterTag);
      });
    }
    
    function filterGames(games, searchTerm, filterTag) {
      const filteredGames = games.filter(function(game) {
        const matchesSearch = !searchTerm || 
          game.title.toLowerCase().includes(searchTerm) || 
          game.description.toLowerCase().includes(searchTerm);
        
        const matchesTag = !filterTag || game.tags.some(tag => tag.toLowerCase().includes(filterTag));
        
        return matchesSearch && matchesTag;
      });
      
      renderGames(filteredGames);
    }
  </script>
</body>
</html>
