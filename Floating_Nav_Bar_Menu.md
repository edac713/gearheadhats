```liquid
<style>
    /* Base styles for floating nav bar menu */
    .floating-menu, .floating-menu-section {
      font-family: sans-serif;
      background-color: rgba(26, 26, 26, 0.725);
      -webkit-backdrop-filter: blur(15px);
      backdrop-filter: blur(10px);
      padding: 20px;
      width: 300px;
      height: 67px;
      z-index: 110 !important;
      position: fixed;
      bottom: 21px;
      left: 50%;
      transform: translateX(-50%);
      border-radius: 22px;
      display: flex;
      justify-content: space-around;
      align-items: center;
      box-shadow: 0 7px 30px rgba(0, 0, 0, 0.5);
    }

    /* Icon styles */
    .floating-menu a, .floating-menu svg, .cart-count-bubble {
      display: flex;
      align-items: center;
      text-align: center;
    }

    /* Styles for the menu toggle */
    #checkbox {
      display: none;
    }

    .toggle {
      position: relative;
      width: 24px;
      cursor: pointer;
      margin: auto;
      display: block;
      height: calc(3px * 3 + 8px * 2);
    }

    .bar {
      display: block !important;
      position: absolute;
      left: 0;
      right: 0;
      height: 3px;
      border-radius: calc(3px / 2);
      background: #FFFFFF;
      transition: none 0.35s cubic-bezier(.5, -0.35, .35, 1.5) 0s;
    }

    .bar--top {
      bottom: calc(50% + 6px + 3px / 2);
      transition-property: bottom, transform;
      transition-delay: calc(0s + 0.35s * .6);
    }

    .bar--middle {
      top: calc(50% - 3px / 2);
      transition-property: opacity, transform;
      transition-delay: calc(0s + 0.35s * .3);
    }

    .bar--bottom {
      top: calc(50% + 6px + 3px / 2);
      transition-property: top, transform;
      transition-delay: 0s;
    }

    #checkbox:checked + .toggle .bar--top {
      transform: rotate(-135deg);
      bottom: calc(50% - 3px / 2);
    }

    #checkbox:checked + .toggle .bar--middle {
      opacity: 0;
      transform: rotate(-135deg);
    }

    #checkbox:checked + .toggle .bar--bottom {
      top: calc(50% - 3px / 2);
      transform: rotate(-225deg);
    }

    /* Cart icon styles */
    .custom-cart-icon {
      position: relative;
    }

    .cart-count-bubble {
      position: absolute;
      top: 0px;
      right: 0px;
      background-color: #f84c43;
      border-radius: 50%;
      width: 20px;
      height: 20px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-size: 12px;
    }

    .icon-container {
      width: 44px;
      height: 44px;
      display: flex;
      justify-content: center;
      align-items: center;
      border: 2px solid transparent;
      border-radius: 12px;
      position: relative;
    }

    .icon-container.selected {}

    .icon-container.selected svg path {
      fill: #FFFFFF !important;
    }

    #home-icon-container.selected svg path {
      stroke: #FFFFFF !important;
    }

    /* Search bar styles */
    .search-bar-container {
      position: fixed;
      bottom: 95px;
      left: 50%;
      transform: translateX(-50%);
      height: 50px;
      width: 300px;
      display: flex;
      align-items: center;
      opacity: 0;
      visibility: hidden;
      transition: all 0.3s ease-in-out;
      border-radius: 50px;
      border-color: rgba(68, 68, 68, 0.5) !important;
      border-width: 2px;
      border-style: solid;
    }

    .search-bar-container.show {
      opacity: 1;
      visibility: visible;
    }

    #search-input {
      width: 100%;
      height: 100%;
      padding: 0 16px;
      background-color: rgba(255, 255, 255, 0.75);
      -webkit-backdrop-filter: blur(15px);
      backdrop-filter: blur(10px);
      font-size: calc(44px * 0.5);
      color: #000000;
      border-radius: 50px;
    }

    /* Empty and filled cart icon styles */
    #empty-cart-icon, #filled-cart-icon {
      min-width: 24px;
      min-height: 24px;
    }

    /* Animated dot styles */
    .dot {
      position: absolute;
      bottom: 0;
      left: 50%;
      transform: translateX(-50%);
      width: 4px;
      height: 4px;
      border-radius: 50%;
      background-color: white;
      opacity: 0;
      transition: all 0.3s ease-in-out;
    }

    .show-dot .dot {
      opacity: 1;
    }

  /* Additional Menu styles */
  #additional-menu {
      position: fixed;
      bottom: 95px;
      left: 50%;
      transform: translateX(-50%) translateY(100%);
      transition: transform 0.3s ease-in-out, opacity 0.3s ease-in-out, visibility 0s 0.3s;
      height: auto;
      width: 300px;
      overflow: hidden;
      border-radius: 22px;
      box-shadow: 0 -7px 20px rgba(0, 0, 0, 0.2);
      opacity: 0;
      visibility: hidden;
      color: #FFFFFF;
      border: 1px solid #D3D3D3;
  }

  #additional-menu.show {
      max-height: 500px;
      opacity: 1;
      visibility: visible;
      transform: translateX(-50%) translateY(0);
      background-color: rgba(26, 26, 26, 0.75);
      -webkit-backdrop-filter: blur(15px);
      backdrop-filter: blur(10px);
      font-size: calc(44px * 0.5);
      font-weight: bold;
      transition: transform 0.3s ease-in-out, opacity 0.3s ease-in-out, visibility 0s;
  }

  #additional-menu a, #additional-menu.show a {
      color: #FFFFFF;
      text-decoration: none;
  }

  #additional-menu ul li a {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 8px 16px;
  }

  .menu-text {
      display: block;
  }

  .up-right-arrow {
      display: inline-block;
      width: 24px;
      height: 24px;

  .up-right-arrow svg {
      display: block;
      width: 100%;
      height: 100%;
  }

  #additional-menu ul {
      list-style-type: none !important;
      padding: 0;
      margin: 0;
  }
</style>

<!-- Floating Menu Section -->
<div id="floating-menu-section">
  <div class="search-bar-container" id="search-bar-container">
    <input type="text" id="search-input" placeholder="Search...">
  </div>

  <!-- Additional Menu -->
  <div id="additional-menu">
    <ul>
      <li>
        <a href="https://gearheadhats.com/collections/patches">
          <span class="menu-text">Patches</span>
          {% render 'up-right-arrow' %}
        </a>
      </li>
      <li>
        <a href="https://gearheadhats.com/collections/hats">
          <span class="menu-text">Hats</span>
          {% render 'up-right-arrow' %}
        </a>
      </li>
      <!-- New Link -->
      <li>
        <a href="https://gearheadhats.com/collections/ready-made">
          <span class="menu-text">Ready Made</span>
          {% render 'up-right-arrow' %}
        </a>
      </li>
      <!-- ...other menu items -->
    </ul>
  </div>

  <nav class="floating-menu">
    <div class="icon-container" id="home-icon-container">
      <a href="https://gearheadhats.com">
        <!-- EMPTY Home Icon -->
        {% render 'empty-home-icon' %}
        <!-- FILLED Home Icon -->
        {% render 'filled-home-icon' %}
      </a>
      <div class="dot">&nbsp;</div>
    </div>

    <div class="icon-container" id="search-icon-container">
      <!-- EMPTY Search Icon -->
      {% render 'empty-search-icon' %}
      <!-- FILLED Search Icon -->
      {% render 'filled-search-icon' %}
      <div class="dot">&nbsp;</div>
    </div>

    <div class="icon-container" id="cart-icon-container">
      <a href="/cart">
        <!-- EMPTY Cart Icon -->
        {% render 'empty-cart-icon' %}
        <!-- FILLED Cart Icon -->
        {% render 'filled-cart-icon' %}
        <div class="cart-count-bubble" id="cart-count-bubble">
          <span id="cart-item-count">0</span>
        </div>
      </a>
      <div class="dot">&nbsp;</div>
    </div>

    <div class="icon-container" id="menu-icon-container">
      <div id="menuToggle">
        <input id="checkbox" type="checkbox">
        <label class="toggle" for="checkbox">
          <div class="bar bar--top"></div>
          <div class="bar bar--middle"></div>
          <div class="bar bar--bottom"></div>
        </label>
      </div>
    </div>
  </nav>
</div>

<script>
  // Function to update cart count and visibility of bubble
  function updateCartCount() {
    fetch('/cart.js')
      .then((response) => response.json())
      .then((cart) => {
        const itemCount = cart.item_count;
        const bubble = document.getElementById('cart-count-bubble');
        const itemCountElement = document.getElementById('cart-item-count');

        const emptyCartIcon = document.getElementById('empty-cart-icon');
        const filledCartIcon = document.getElementById('filled-cart-icon');

        itemCountElement.innerText = itemCount;

        if (itemCount > 0) {
          bubble.style.display = 'flex';
          filledCartIcon.style.display = 'block';
          emptyCartIcon.style.display = 'none';
        } else {
          bubble.style.display = 'none';
          filledCartIcon.style.display = 'none';
          emptyCartIcon.style.display = 'block';
        }
      });
  }

  // Initial cart count update
  updateCartCount();

  // Function to update the 'selected' state of the icon containers
  function updateSelectedIcon(selectedId) {
    // Remove the 'selected' class and dot from all icon containers
    document.querySelectorAll('.icon-container').forEach((container) => {
      container.classList.remove('selected');
      container.classList.remove('show-dot');
    });

    // Add the 'selected' class and dot to the selected icon container
    document.getElementById(selectedId).classList.add('selected');
    document.getElementById(selectedId).classList.add('show-dot');
  }

  // Initial update based on current URL
  const currentUrl = window.location.href;
  if (currentUrl.includes('gearheadhats.com') && !currentUrl.includes('/search') && !currentUrl.includes('/cart')) {
    updateSelectedIcon('home-icon-container');
  } else {
    document.getElementById('home-icon-container').classList.remove('selected');
    if (currentUrl.includes('/search')) {
      updateSelectedIcon('search-icon-container');
    } else if (currentUrl.includes('/cart')) {
      updateSelectedIcon('cart-icon-container');
    }
  }

  // Event listeners for icon clicks
  document
    .getElementById('home-icon-container')
    .addEventListener('click', () => updateSelectedIcon('home-icon-container'));

  const searchBarContainer = document.getElementById('search-bar-container');
  const searchIcon = document.getElementById('search-icon-container');
  const emptySearchIcon = document.getElementById('empty-search-icon');
  const filledSearchIcon = document.getElementById('filled-search-icon');

  // Toggle search bar and icon when search icon is clicked
  searchIcon.addEventListener('click', function (e) {
    e.stopPropagation();
    searchBarContainer.classList.toggle('show');

    // Toggle between empty and filled search icons
    if (searchBarContainer.classList.contains('show')) {
      emptySearchIcon.style.display = 'none';
      filledSearchIcon.style.display = 'block';
    } else {
      emptySearchIcon.style.display = 'block';
      filledSearchIcon.style.display = 'none';
    }
  });

  // Hide search bar when clicked outside
  document.addEventListener('click', function () {
    searchBarContainer.classList.remove('show');

    // Set the search icon back to its empty state
    emptySearchIcon.style.display = 'block';
    filledSearchIcon.style.display = 'none';
  });

  // Prevent hiding when clicking inside the search bar
  searchBarContainer.addEventListener('click', function (e) {
    e.stopPropagation();
  });

  document
    .getElementById('cart-icon-container')
    .addEventListener('click', () => updateSelectedIcon('cart-icon-container'));

  // Listen to changes in the browser's history
  window.addEventListener('popstate', () => {
    const newUrl = window.location.href;
    if (newUrl.includes('gearheadhats.com') && !newUrl.includes('/search') && !newUrl.includes('/cart')) {
      updateSelectedIcon('home-icon-container');
    }
  });

  // Get the search input element
  const searchInput = document.getElementById('search-input');

  // Add an event listener for the "keyup" event on the search input
  searchInput.addEventListener('keyup', function (event) {
    // Check if the "Enter" key was pressed
    if (event.key === 'Enter') {
      // Prevent any default action
      event.preventDefault();

      // Get the search query from the input
      const query = searchInput.value;

      // Redirect to the Shopify search results page for the query
      window.location.href = `/search?q=${encodeURIComponent(query)}`;
    }
  });

  // Get the menu toggle checkbox element
  const menuToggleCheckbox = document.getElementById('checkbox');
  const additionalMenu = document.getElementById('additional-menu');

  // Add an event listener to the checkbox to toggle the additional menu
  menuToggleCheckbox.addEventListener('change', () => {
    if (menuToggleCheckbox.checked) {
      additionalMenu.classList.add('show');
    } else {
      additionalMenu.classList.remove('show');
    }
  });
</script>
```
