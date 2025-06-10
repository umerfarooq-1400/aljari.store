<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title id="mainTitle">Al Jari - High Quality Kufis</title>

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>

    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Playfair+Display:wght@700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">

    <!-- Custom Styles -->
    <style>
        /* Base font settings and background transition */
        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(to bottom, #111827, #000000, #0c1a3a); /* Default fallback gradient */
            color: white;
            transition: background-color 0.3s ease; /* Smooth background transition */
            overflow-x: hidden; /* Prevent horizontal scroll */
        }
        /* Specific font for login screen */
        #loginScreen {
            font-family: 'Inter', sans-serif;
        }
        /* Specific font for titles */
        .font-playfair {
            font-family: 'Playfair Display', serif;
        }
        .font-poppins {
            font-family: 'Poppins', sans-serif;
        }
        .font-inter {
            font-family: 'Inter', sans-serif;
        }

        /* Hero section background image */
        .hero-bg {
            background-image: url('https://source.unsplash.com/random/1600x900?islamic-pattern');
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
        }
        /* Page transition animation for smooth navigation */
        .page-section {
            display: none; /* Hidden by default */
            animation: fadeIn 0.5s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        /* Product card hover effect for visual feedback */
        .product-card {
            transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
        }
        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
        }
        /* Custom styling for the color picker input */
        input[type="color"]::-webkit-color-swatch-wrapper {
            padding: 0;
        }
        input[type="color"]::-webkit-color-swatch {
            border: none;
            border-radius: 9999px; /* For rounded swatch */
        }
        input[type="color"] {
            -webkit-appearance: none;
            -moz-appearance: none;
            appearance: none;
            width: 40px;
            height: 40px;
            background-color: transparent;
            border: none;
            cursor: pointer;
            border-radius: 9999px; /* Ensure input itself is rounded */
        }
        /* Styling for transient message box */
        .message-box {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 1000;
            padding: 10px 20px;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            opacity: 0;
            animation: fadeInOut 3s forwards;
            color: white; /* Ensure text is white */
            background-color: #4CAF50; /* Default success color */
        }
        .message-box.error {
            background-color: #f44336; /* Error color */
        }
        /* Keyframe animation for message box fade in/out */
        @keyframes fadeInOut {
            0% { opacity: 0; transform: translateX(-50%) translateY(-10px); }
            10% { opacity: 1; transform: translateX(-50%) translateY(0); }
            90% { opacity: 1; transform: translateX(-50%) translateY(0); }
            100% { opacity: 0; transform: translateX(-50%) translateY(-10px); }
        }

        /* Admin panel slide-in animation */
        #adminPanel.slide-in {
            animation: slideInRight 0.5s forwards;
            display: block; /* Ensure it's block for animation */
        }
        #adminPanel.slide-out {
            animation: slideOutRight 0.5s forwards;
        }

        @keyframes slideInRight {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        @keyframes slideOutRight {
            from { transform: translateX(0); opacity: 1; }
            to { transform: translateX(100%); opacity: 0; }
        }
    </style>
</head>
<body class="bg-gray-900 text-white">

    <!-- Custom Message Box for user feedback -->
    <div id="messageBox" class="message-box hidden"></div>

    <!-- Login Screen - first screen shown to user -->
    <div id="loginScreen" class="flex items-center justify-center min-h-screen">
        <div class="w-full max-w-md p-8 space-y-8 bg-gray-800 rounded-2xl shadow-2xl">
            <!-- Login screen header -->
            <div class="text-center">
                <h1 class="text-4xl font-bold text-white font-playfair">Al Jari</h1>
                <p class="mt-2 text-gray-400 font-poppins">Please enter the password to continue</p>
            </div>

            <!-- Login Form -->
            <form onsubmit="checkPassword(event)">
                <div class="space-y-6">
                    <!-- Password Input Field -->
                    <div>
                        <label for="password" class="sr-only">Password</label>
                        <div class="relative">
                            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                                <!-- Lock Icon for password field -->
                                <svg class="h-5 w-5 text-gray-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                                    <path fill-rule="evenodd" d="M10 1a4.5 4.5 0 00-4.5 4.5V9H5a2 2 0 00-2 2v6a2 2 0 002 2h10a2 2 0 002-2v-6a2 2 0 00-2-2h-.5V5.5A4.5 4.5 0 0010 1zm3 8V5.5a3 3 0 10-6 0V9h6z" clip-rule="evenodd" />
                                </svg>
                            </div>
                            <input type="password" id="password" placeholder="Password" required class="w-full pl-10 pr-4 py-3 bg-gray-700 border border-gray-600 rounded-lg text-white placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent transition font-inter">
                        </div>
                    </div>
                    <!-- Error Message for incorrect password -->
                    <div id="errorMessage" class="hidden text-center text-red-400 text-sm font-medium p-3 bg-red-500 bg-opacity-10 rounded-lg">
                        Incorrect password. Please try again.
                    </div>
                    <!-- Submit Button for login -->
                    <div>
                        <button type="submit" class="w-full px-4 py-3 font-semibold text-white bg-blue-600 rounded-lg hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-blue-500 transition duration-300 font-poppins">
                            Enter
                        </button>
                    </div>
                </div>
            </form>
        </div>
    </div>

    <!-- Main Website Content - hidden until password is entered -->
    <div id="mainContent" class="hidden">
        <!-- Header & Navigation Bar -->
        <header class="bg-black bg-opacity-30 backdrop-blur-sm sticky top-0 z-50">
            <nav class="container mx-auto px-6 py-4 flex flex-col md:flex-row justify-between items-center">
                <a href="#" onclick="showPage('home')" class="text-3xl font-playfair font-bold text-white mb-4 md:mb-0">Al Jari</a>
                <ul class="flex items-center space-x-6">
                    <li><a href="#" onclick="showPage('home')" class="nav-link text-lg hover:text-indigo-400 transition-colors font-poppins">Home</a></li>
                    <li><a href="#" onclick="showPage('products')" class="nav-link text-lg hover:text-indigo-400 transition-colors font-poppins">Products</a></li>
                    <li><a href="#" onclick="showPage('about')" class="nav-link text-lg hover:text-indigo-400 transition-colors font-poppins">About</a></li>
                    <li><a href="#" onclick="showPage('contact')" class="nav-link text-lg hover:text-indigo-400 transition-colors font-poppins">Contact</a></li>
                </ul>
            </nav>
        </header>
        
        <!-- Edit Mode Toggle Button - fixed position for easy access -->
        <button id="editToggle" class="fixed top-20 right-6 bg-gradient-to-br from-indigo-500 to-purple-600 text-white px-4 py-2 rounded-lg shadow-lg hover:from-indigo-600 hover:to-purple-700 transition-all transform hover:scale-105 z-40 font-poppins">
            🛠 Edit Mode
        </button>

        <!-- Admin Panel - slides out from the right when edit mode is active -->
        <div id="adminPanel" class="hidden fixed top-0 right-0 h-full bg-white text-gray-800 p-6 rounded-l-xl shadow-2xl w-96 z-40 space-y-6 overflow-y-auto transform translate-x-full transition-transform duration-500 ease-in-out">
            <h3 class="font-bold text-2xl mb-4 text-center font-playfair">Customize Website</h3>

            <!-- Global Settings Section -->
            <div class="border-b pb-4 mb-4">
                <h4 class="font-semibold text-lg mb-3 font-poppins">Global Settings:</h4>
                <label for="mainTitleInput" class="font-semibold block mb-2 font-poppins">Website Title:</label>
                <input type="text" id="mainTitleInput" placeholder="Enter new title" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter">

                <label for="headerTitleInput" class="font-semibold block mb-2 font-poppins">Header Title:</label>
                <input type="text" id="headerTitleInput" placeholder="Enter header title" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter">

                <label for="footerTextInput" class="font-semibold block mb-2 font-poppins">Footer Text:</label>
                <input type="text" id="footerTextInput" placeholder="Enter footer text" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter">

                <label for="heroImageUrlInput" class="font-semibold block mb-2 font-poppins">Hero Background Image URL:</label>
                <input type="text" id="heroImageUrlInput" placeholder="https://unsplash.com/image.jpg" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter">

                <div class="flex items-center justify-between mb-3">
                    <label for="backgroundColorInput" class="font-semibold font-poppins">Background Color:</label>
                    <input type="color" id="backgroundColorInput" value="#111827"
                            class="w-10 h-10 border-none rounded-full cursor-pointer shadow-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                </div>

                <div class="flex items-center justify-between mb-3">
                    <label for="bodyFontSelect" class="font-semibold font-poppins">Body Font:</label>
                    <select id="bodyFontSelect" class="p-2 border border-gray-300 rounded-md font-inter">
                        <option value="Poppins, sans-serif">Poppins</option>
                        <option value="Inter, sans-serif">Inter</option>
                        <option value="Playfair Display, serif">Playfair Display</option>
                    </select>
                </div>
                <div class="flex items-center justify-between">
                    <label for="headingFontSelect" class="font-semibold font-poppins">Heading Font:</label>
                    <select id="headingFontSelect" class="p-2 border border-gray-300 rounded-md font-inter">
                        <option value="Playfair Display, serif">Playfair Display</option>
                        <option value="Poppins, sans-serif">Poppins</option>
                        <option value="Inter, sans-serif">Inter</option>
                    </select>
                </div>
            </div>

            <!-- Page Content Editing Section -->
            <div class="border-b pb-4 mb-4">
                <h4 class="font-semibold text-lg mb-3 font-poppins">Page Content:</h4>
                
                <label for="homeHeroTitleInput" class="font-semibold block mb-2 font-poppins">Home Hero Title:</label>
                <input type="text" id="homeHeroTitleInput" placeholder="Enter new hero title" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter">

                <label for="homeHeroDescriptionInput" class="font-semibold block mb-2 font-poppins">Home Hero Description:</label>
                <textarea id="homeHeroDescriptionInput" placeholder="Enter new hero description" rows="3" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter"></textarea>

                <label for="productsPageHeadingInput" class="font-semibold block mb-2 font-poppins">Products Page Heading:</label>
                <input type="text" id="productsPageHeadingInput" placeholder="Enter new products heading" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter">

                <label for="aboutPageHeadingInput" class="font-semibold block mb-2 font-poppins">About Page Heading:</label>
                <input type="text" id="aboutPageHeadingInput" placeholder="Enter new about heading" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter">

                <label for="contactPageHeadingInput" class="font-semibold block mb-2 font-poppins">Contact Page Heading:</label>
                <input type="text" id="contactPageHeadingInput" placeholder="Enter new contact heading" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter">

                <label for="editableText" class="font-semibold block mb-1 font-poppins">About Us Page Text:</label>
                <textarea id="editableText" placeholder="Enter new 'About Us' text" class="w-full p-2 border border-gray-300 rounded-md focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 transition font-inter" rows="5"></textarea>
                <button onclick="editContent()" class="mt-3 w-full bg-indigo-600 text-white py-2 rounded-md hover:bg-indigo-700 transition-colors font-poppins">Update About Text</button>

                <!-- New inputs for Example Kufis Section -->
                <h5 class="font-semibold text-md mt-6 mb-3 font-poppins">Example Kufi Section:</h5>
                <label for="exampleKufiHeadingInput" class="font-semibold block mb-2 font-poppins">Example Kufi Heading:</label>
                <input type="text" id="exampleKufiHeadingInput" placeholder="e.g., Daily Wear Kufis" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter">
                <label for="exampleKufiDescriptionInput" class="font-semibold block mb-2 font-poppins">Example Kufi Description:</label>
                <textarea id="exampleKufiDescriptionInput" placeholder="Description for daily wear kufis" rows="2" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter"></textarea>
                <label for="exampleKufiImageUrlInput" class="font-semibold block mb-2 font-poppins">Example Kufi Image URL:</label>
                <input type="text" id="exampleKufiImageUrlInput" placeholder="https://placehold.co/600x400" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter">

                <!-- New inputs for Unique Kufis Section -->
                <h5 class="font-semibold text-md mt-6 mb-3 font-poppins">Unique Kufi Section:</h5>
                <label for="uniqueKufiHeadingInput" class="font-semibold block mb-2 font-poppins">Unique Kufi Heading:</label>
                <input type="text" id="uniqueKufiHeadingInput" placeholder="e.g., Exclusive Designs" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter">
                <label for="uniqueKufiDescriptionInput" class="font-semibold block mb-2 font-poppins">Unique Kufi Description:</label>
                <textarea id="uniqueKufiDescriptionInput" placeholder="Description for unique designs" rows="2" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter"></textarea>
                <label for="uniqueKufiImageUrlInput" class="font-semibold block mb-2 font-poppins">Unique Kufi Image URL:</label>
                <input type="text" id="uniqueKufiImageUrlInput" placeholder="https://placehold.co/600x400" class="w-full p-2 border border-gray-300 rounded-md mb-3 focus:ring-2 focus:ring-indigo-500 font-inter">

            </div>

            <!-- Product Management Section (Add/Edit) -->
            <div>
                <h4 class="font-semibold text-lg mb-3 font-poppins" id="productFormHeading">Add New Product:</h4>
                <input type="text" id="productName" placeholder="Product Name" class="w-full p-2 border border-gray-300 rounded-md mb-2 focus:ring-2 focus:ring-indigo-500 font-inter">
                <input type="text" id="productImageUrl" placeholder="Image URL (e.g., https://placehold.co/400x300)" class="w-full p-2 border border-gray-300 rounded-md mb-2 focus:ring-2 focus:ring-indigo-500 font-inter">
                <textarea id="productDescription" placeholder="Product Description" rows="3" class="w-full p-2 border border-gray-300 rounded-md mb-2 focus:ring-2 focus:ring-indigo-500 font-inter"></textarea>
                <input type="text" id="productSizes" placeholder="Sizes (comma-separated: S,M,L)" class="w-full p-2 border border-gray-300 rounded-md mb-2 focus:ring-2 focus:ring-indigo-500 font-inter">
                <input type="number" id="productPrice" placeholder="Price (e.g., 29.99)" step="0.01" class="w-full p-2 border border-gray-300 rounded-md mb-4 focus:ring-2 focus:ring-indigo-500 font-inter">
                
                <div class="flex space-x-2">
                    <button id="addProductButton" onclick="handleAddOrUpdateProduct()" class="flex-1 bg-green-600 text-white py-2 rounded-md hover:bg-green-700 transition-colors font-poppins">Add Product</button>
                    <button id="cancelProductEditButton" onclick="cancelProductEdit()" class="flex-1 bg-gray-500 text-white py-2 rounded-md hover:bg-gray-600 transition-colors hidden font-poppins">Cancel</button>
                </div>
            </div>

            <button onclick="saveAllSettings()" class="mt-6 w-full bg-blue-600 text-white py-3 rounded-md hover:bg-blue-700 transition-colors font-poppins shadow-lg">Save All Changes</button>
        </div>
        
        <!-- Main Content Area - contains all the pages -->
        <main class="container mx-auto px-6 py-8">
            <!-- Home Page Section -->
            <section id="home" class="page-section">
                <div class="hero-bg h-[60vh] rounded-2xl flex flex-col items-center justify-center text-center p-8 relative">
                    <div class="absolute inset-0 bg-black bg-opacity-60 rounded-2xl"></div>
                    <div class="relative z-10">
                        <h1 id="homeHeroTitle" class="text-5xl md:text-6xl font-playfair font-bold text-white shadow-lg leading-tight">Elegance in Every Stitch</h1>
                        <p id="homeHeroDescription" class="text-xl md:text-2xl mt-4 font-light text-gray-200 font-poppins">Discover our exclusive collection of high-quality Kufis.</p>
                        <button onclick="showPage('products')" class="mt-8 bg-gradient-to-br from-indigo-500 to-purple-600 text-white font-bold py-3 px-8 rounded-lg shadow-lg hover:from-indigo-600 hover:to-purple-700 transition-all transform hover:scale-105 font-poppins">
                            View Collection
                        </button>
                    </div>
                </div>

                <!-- Section for Unique Hard Kufi -->
                <div class="mt-16 py-12 px-8 bg-gradient-to-tr from-gray-800 to-gray-900 rounded-xl shadow-2xl text-center">
                    <h2 class="text-4xl font-playfair font-bold text-white mb-6">Our Special Selection</h2>
                    <p class="text-lg text-gray-300 mb-8 max-w-2xl mx-auto font-poppins">
                        Discover the exquisite craftsmanship of our unique hard kufi, designed for unparalleled elegance and comfort.
                    </p>
                    <div class="flex flex-col md:flex-row items-center justify-center gap-8">
                        <div class="w-full md:w-1/2 lg:w-1/3">
                            <img src="https://placehold.co/600x400/2D3748/FFFFFF?text=Unique+Hard+Kufi" 
                                 alt="Unique Hard Kufi" 
                                 class="rounded-xl shadow-lg transform transition-transform duration-300 hover:scale-105 w-full object-cover aspect-video">
                        </div>
                        <div class="w-full md:w-1/2 lg:w-1/3 text-left">
                            <h3 class="text-3xl font-playfair font-bold text-indigo-400 mb-4">The Artisan's Choice</h3>
                            <p class="text-gray-300 leading-relaxed font-poppins">
                                This handcrafted hard kufi features intricate embroidery and a durable structure, perfect for daily wear or special occasions. Its unique design stands as a testament to traditional artistry blended with modern comfort. A timeless piece for every discerning individual.
                            </p>
                            <button onclick="showPage('products')" class="mt-6 bg-gradient-to-br from-purple-600 to-indigo-500 text-white font-bold py-3 px-6 rounded-lg shadow-md hover:from-purple-700 hover:to-indigo-600 transition-all transform hover:scale-105 font-poppins">
                                Explore More
                            </button>
                        </div>
                    </div>
                </div>

                <!-- New Section for Example Kufis -->
                <div class="mt-16 py-12 px-8 bg-gradient-to-tl from-gray-800 to-gray-900 rounded-xl shadow-2xl text-center">
                    <h2 id="exampleKufiHeading" class="text-4xl font-playfair font-bold text-white mb-6">Daily Wear Kufis</h2>
                    <p id="exampleKufiDescription" class="text-lg text-gray-300 mb-8 max-w-2xl mx-auto font-poppins">
                        Our collection of comfortable and stylish kufis perfect for everyday use.
                    </p>
                    <div class="w-full max-w-xl mx-auto">
                        <img id="exampleKufiImage" src="https://placehold.co/600x400/374151/FFFFFF?text=Example+Kufi+1" 
                             alt="Example Kufi 1" 
                             class="rounded-xl shadow-lg transform transition-transform duration-300 hover:scale-105 w-full object-cover aspect-video">
                    </div>
                </div>

                <!-- New Section for Another Unique Kufi -->
                <div class="mt-16 py-12 px-8 bg-gradient-to-br from-gray-800 to-gray-900 rounded-xl shadow-2xl text-center">
                    <h2 id="uniqueKufiHeading" class="text-4xl font-playfair font-bold text-white mb-6">Exclusive Designs</h2>
                    <p id="uniqueKufiDescription" class="text-lg text-gray-300 mb-8 max-w-2xl mx-auto font-poppins">
                        Explore our limited edition kufis featuring bespoke designs and premium materials.
                    </p>
                    <div class="w-full max-w-xl mx-auto">
                        <img id="uniqueKufiImage" src="https://placehold.co/600x400/2D3748/FFFFFF?text=Unique+Kufi+2" 
                             alt="Unique Kufi 2" 
                             class="rounded-xl shadow-lg transform transition-transform duration-300 hover:scale-105 w-full object-cover aspect-video">
                    </div>
                </div>

            </section>
            <!-- Products Page Section -->
            <section id="products" class="page-section">
                <h2 id="productsPageHeading" class="text-4xl font-playfair font-bold text-center mb-8">Our Collection</h2>
                <div id="product-list" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8">
                    <!-- Products will be dynamically inserted here by JavaScript -->
                    <p id="no-products-message" class="col-span-full text-center text-gray-400 text-xl hidden font-poppins">No products added yet. Use the Edit Mode to add some!</p>
                </div>
            </section>
            <!-- About Us Page Section -->
            <section id="about" class="page-section">
                <div class="max-w-3xl mx-auto bg-white bg-opacity-10 backdrop-blur-md p-8 rounded-xl shadow-lg">
                    <h2 id="aboutPageHeading" class="text-4xl font-playfair font-bold text-center mb-6">About Al Jari</h2>
                    <p id="editable-section" class="text-lg text-gray-200 leading-relaxed font-poppins">
                        Al Jari specializes in making out high quality kufis. Each piece is crafted with meticulous care, reflecting a rich heritage of tradition and faith. We believe our products are more than just headwear; they are a symbol of identity and devotion.
                    </p>
                </div>
            </section>
            <!-- Contact Page Section -->
            <section id="contact" class="page-section">
                <div class="max-w-2xl mx-auto bg-white bg-opacity-10 backdrop-blur-md p-8 rounded-xl shadow-lg">
                    <h2 id="contactPageHeading" class="text-4xl font-playfair font-bold text-center mb-6">Contact Us</h2>
                    <form id="contactForm" class="space-y-6">
                        <input type="text" placeholder="Your Name" required class="w-full p-3 bg-gray-700 border border-gray-600 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 outline-none transition font-inter">
                        <input type="email" placeholder="Your Email" required class="w-full p-3 bg-gray-700 border border-gray-600 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 outline-none transition font-inter">
                        <textarea placeholder="Your Message" rows="5" class="w-full p-3 bg-gray-700 border border-gray-600 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 outline-none transition resize-none font-inter"></textarea>
                        <button type="submit" class="w-full bg-gradient-to-br from-indigo-500 to-purple-600 text-white font-bold py-3 px-6 rounded-lg shadow-lg hover:from-indigo-600 hover:to-purple-700 transition-all font-poppins">Send Message</button>
                    </form>
                </div>
            </section>
        </main>
        
        <!-- Footer -->
        <footer class="text-center py-8 mt-12 bg-[#0c1a3a]">
            <p id="footerText" class="text-gray-400 font-poppins">&copy; 2025 Al Jari - All Rights Reserved</p>
            <p id="footerUserId" class="text-xs text-gray-400 mt-2 hidden font-inter"></p>
        </footer>
    </div>

    <!-- Custom Alert Modal - for general messages -->
    <div id="customModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-[60]">
        <div class="bg-white text-gray-800 p-8 rounded-lg shadow-xl text-center w-full max-w-sm">
            <p id="modalMessage" class="mb-4 text-lg font-poppins"></p>
            <button onclick="closeModal()" class="bg-indigo-600 text-white px-6 py-2 rounded-md hover:bg-indigo-700 transition-colors font-poppins">OK</button>
        </div>
    </div>

    <!-- Custom Confirmation Modal - for delete operations -->
    <div id="confirmationModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-[60]">
        <div class="bg-white text-gray-800 p-8 rounded-lg shadow-xl text-center w-full max-w-sm">
            <p id="confirmationMessage" class="mb-6 text-lg font-poppins">Are you sure you want to delete this item?</p>
            <div class="flex justify-center space-x-4">
                <button onclick="cancelDelete()" class="px-6 py-2 rounded-md bg-gray-200 hover:bg-gray-300 transition-colors font-poppins">Cancel</button>
                <button onclick="confirmDelete()" class="px-6 py-2 rounded-md bg-red-600 text-white hover:bg-red-700 transition-colors font-poppins">Delete</button>
            </div>
        </div>
    </div>

    <script>
        // --- Password Check Function for initial access ---
        function checkPassword(event) {
            event.preventDefault(); // Prevent default form submission behavior
            
            const passwordInput = document.getElementById("password");
            const errorMessage = document.getElementById("errorMessage");
            const correctPassword = "MercedesAMG999"; // 🔐 IMPORTANT: Change this to your desired password for website access

            if (passwordInput.value === correctPassword) {
                // If password is correct, hide login and show main content
                document.getElementById("loginScreen").classList.add('hidden');
                document.getElementById("mainContent").classList.remove('hidden');
                
                // Initialize the main website functionality after successful login
                initializeAppLogic();
            } else {
                // Show error message for incorrect password
                errorMessage.classList.remove('hidden');
                passwordInput.value = ""; // Clear input for security
                setTimeout(() => {
                    errorMessage.classList.add('hidden');
                }, 3000); // Hide error after 3 seconds
            }
        }

        // --- Custom Modal Functions (replacing alert/confirm) ---
        function showModal(message) {
            const modal = document.getElementById('customModal');
            document.getElementById('modalMessage').textContent = message;
            modal.classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('customModal').classList.add('hidden');
        }

        let pendingDeleteAction = null; // Stores the function to execute on confirmation

        function showConfirmationModal(message, onConfirm) {
            const modal = document.getElementById('confirmationModal');
            document.getElementById('confirmationMessage').textContent = message;
            pendingDeleteAction = onConfirm; // Store the callback
            modal.classList.remove('hidden');
        }

        function confirmDelete() {
            if (pendingDeleteAction) {
                pendingDeleteAction(); // Execute the stored callback
                pendingDeleteAction = null; // Clear it
            }
            document.getElementById('confirmationModal').classList.add('hidden');
        }

        function cancelDelete() {
            pendingDeleteAction = null; // Clear the callback
            document.getElementById('confirmationModal').classList.add('hidden');
        }
    </script>
    
    <!-- Firebase and Main App Logic (Module Script for ES6 imports) -->
    <script type="module">
        // Firebase Imports - essential for database and authentication
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, onAuthStateChanged, signInWithCustomToken } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, onSnapshot, collection, addDoc, deleteDoc, setDoc, updateDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Global variables to store Firebase instances and app state
        let db;
        let auth;
        let userId; // Current authenticated user ID
        let productsCollectionRef; // Firestore collection reference for products
        let contentDocRef; // Firestore document reference for "About Us" content
        let settingsDocRef; // Firestore document reference for global site settings (titles, colors)
        let productToDeleteId = null; // Stores ID of product targeted for deletion
        let productToEditId = null; // Stores ID of product currently being edited
        let messageTimeoutRef = null; // Timer for transient message box

        // Function to display transient messages (success/error) to the user
        function showMessage(msg, isError = false) {
            const messageBox = document.getElementById('messageBox');
            if (messageBox) { // Ensure messageBox exists before trying to modify it
                messageBox.textContent = msg;
                messageBox.classList.remove('hidden', 'bg-blue-500', 'bg-red-500'); // Clean previous state
                messageBox.classList.add(isError ? 'bg-red-500' : 'bg-blue-500'); // Apply success or error style
                messageBox.style.animation = 'none'; // Reset CSS animation
                void messageBox.offsetWidth; // Trigger reflow to restart animation
                messageBox.style.animation = 'fadeInOut 3s forwards'; // Start fade animation

                if (messageTimeoutRef) {
                    clearTimeout(messageTimeoutRef); // Clear any previous timeout
                }
                messageTimeoutRef = setTimeout(() => {
                    messageBox.classList.add('hidden'); // Hide message after 3 seconds
                }, 3000); 
            } else {
                console.warn("Message box element not found."); // Log if element is missing
            }
        }

        // --- Main App Initialization - called after password authentication ---
        window.initializeAppLogic = () => {
            // Retrieve Firebase configuration from global __firebase_config variable
            const firebaseConfig = typeof __firebase_config !== 'undefined' 
                ? JSON.parse(__firebase_config)
                : {}; // Fallback to empty object if not defined

            // Initialize Firebase app, authentication, and Firestore database
            const app = initializeApp(firebaseConfig);
            auth = getAuth(app);
            db = getFirestore(app);

            // --- Firebase Authentication State Listener ---
            // Listens for changes in the user's authentication state (login/logout)
            onAuthStateChanged(auth, async (user) => {
                if (user) {
                    console.log("User is signed in with UID:", user.uid);
                    userId = user.uid; // Set global userId
                    // Display user ID in footer for multi-user context
                    const footerUserIdEl = document.getElementById("footerUserId");
                    if (footerUserIdEl) {
                        footerUserIdEl.textContent = `User ID: ${userId}`;
                        footerUserIdEl.classList.remove('hidden');
                    }
                    // Setup Firestore references and load data once authenticated
                    setupFirestoreRefs();
                    loadContent();
                    loadProducts();
                    loadSettings(); 
                } else {
                    console.log("User not signed in, attempting authentication...");
                    try {
                        // Attempt to sign in with custom token provided by the environment
                        if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                            await signInWithCustomToken(auth, __initial_auth_token);
                            console.log("Signed in with custom token.");
                        } else {
                            // If no custom token, sign in anonymously
                            await signInAnonymously(auth);
                            console.log("Signed in anonymously.");
                        }
                        // The onAuthStateChanged listener will re-fire with the new user state
                    } catch (error) {
                        console.error("Authentication failed:", error);
                        showMessage(`Authentication failed: ${error.message}`, true);
                    }
                }
            });

            // Show the home page by default when the app logic initializes
            showPage('home'); 
        };
        
        // --- Firestore References Setup ---
        // Defines the paths to Firestore collections and documents based on app ID and user ID
        function setupFirestoreRefs() {
            if (!userId) return; // Ensure userId is available before setting up references
            const appId = typeof __app_id !== 'undefined' ? __app_id : 'al-jari-website-default'; // Use provided app ID or a default

            // Publicly accessible content documents
            contentDocRef = doc(db, 'artifacts', appId, 'public', 'data', 'site_data', 'about_us_content');
            settingsDocRef = doc(db, 'artifacts', appId, 'public', 'data', 'site_data', 'global_settings');
            productsCollectionRef = collection(db, 'artifacts', appId, 'public', 'data', 'products');
        }

        // --- Page Navigation Function ---
        // Hides all page sections and displays the requested one
        window.showPage = (pageId) => {
            document.querySelectorAll('.page-section').forEach(section => {
                section.style.display = 'none'; // Hide all sections
            });
            const activePage = document.getElementById(pageId);
            if (activePage) {
                activePage.style.display = 'block'; // Show the selected section
            }
        };

        // --- UI & Event Listeners ---
        // Toggles the visibility and animation of the admin panel
        document.getElementById("editToggle").addEventListener("click", () => {
            const adminPanel = document.getElementById("adminPanel");
            const editToggle = document.getElementById("editToggle");
            
            // Check current state for animation control
            const isHidden = adminPanel.classList.contains('hidden') || adminPanel.classList.contains('slide-out');

            if (isHidden) {
                adminPanel.classList.remove('hidden', 'slide-out');
                adminPanel.classList.add('slide-in');
                editToggle.innerHTML = "❌ Close Edit";
            } else {
                adminPanel.classList.remove('slide-in');
                adminPanel.classList.add('slide-out');
                // Hide after animation completes
                adminPanel.addEventListener('animationend', () => {
                    adminPanel.classList.add('hidden');
                }, { once: true });
                editToggle.innerHTML = "🛠 Edit Mode";
            }

            cancelProductEdit(); // Reset product edit form when toggling admin panel

            // Toggle visibility of admin controls on product cards (edit/delete buttons)
            const productControls = document.querySelectorAll('.product-card .admin-controls');
            productControls.forEach(control => {
                if (isHidden) {
                    control.classList.remove('hidden'); // Show controls if admin panel is becoming visible
                } else {
                    control.classList.add('hidden'); // Hide controls if admin panel is becoming hidden
                }
            });
        });
        
        // Event listener for the contact form submission
        document.getElementById("contactForm").addEventListener("submit", (e) => {
            e.preventDefault(); // Prevent default form submission
            showModal("Thank you for your message! We will get back to you soon."); // Show confirmation modal
            e.target.reset(); // Clear the form fields
        });

        // --- Data Loading Functions ---

        // Loads and displays the "About Us" page content from Firestore
        function loadContent() {
            if (!contentDocRef) return; // Exit if Firestore reference is not ready
            onSnapshot(contentDocRef, (docSnap) => {
                const aboutTextEl = document.getElementById("editable-section");
                const editableTextarea = document.getElementById("editableText");
                if (docSnap.exists()) {
                    const data = docSnap.data();
                    aboutTextEl.innerText = data.aboutText || "Default 'About Us' content goes here. Use the edit mode to change this text.";
                    editableTextarea.value = data.aboutText || ""; // Populate textarea for editing
                } else {
                    // Set default text if document doesn't exist
                    aboutTextEl.innerText = "Default 'About Us' content goes here. Use the edit mode to change this text.";
                    editableTextarea.value = "";
                }
            }, (error) => {
                console.error("Error fetching about content:", error);
                showMessage("Error loading About Us content.", true);
            });
        }
        
        // Loads and applies global website settings (titles, background color, fonts) from Firestore
        function loadSettings() {
            if (!settingsDocRef) return; // Exit if Firestore reference is not ready
            onSnapshot(settingsDocRef, (docSnap) => {
                const mainTitleEl = document.getElementById("mainTitle");
                const mainTitleInput = document.getElementById("mainTitleInput");
                const headerTitleInput = document.getElementById("headerTitleInput");
                const footerTextInput = document.getElementById("footerTextInput");
                const backgroundColorInput = document.getElementById("backgroundColorInput");
                const heroImageUrlInput = document.getElementById("heroImageUrlInput");
                const bodyFontSelect = document.getElementById("bodyFontSelect");
                const headingFontSelect = document.getElementById("headingFontSelect");

                const body = document.body;
                const heroBg = document.querySelector(".hero-bg");
                const homeHeroTitleEl = document.getElementById("homeHeroTitle");
                const homeHeroDescriptionEl = document.getElementById("homeHeroDescription");
                const homeHeroTitleInput = document.getElementById("homeHeroTitleInput");
                const homeHeroDescriptionInput = document.getElementById("homeHeroDescriptionInput");
                const productsPageHeadingEl = document.getElementById("productsPageHeading");
                const productsPageHeadingInput = document.getElementById("productsPageHeadingInput");
                const aboutPageHeadingEl = document.getElementById("aboutPageHeading");
                const aboutPageHeadingInput = document.getElementById("aboutPageHeadingInput");
                const contactPageHeadingEl = document.getElementById("contactPageHeading");
                const contactPageHeadingInput = document.getElementById("contactPageHeadingInput");
                const headerTitleEl = document.querySelector("header nav a"); // Selects the "Al Jari" link in the header
                const footerTextEl = document.getElementById("footerText");

                // New elements for additional home page sections
                const exampleKufiHeadingEl = document.getElementById("exampleKufiHeading");
                const exampleKufiDescriptionEl = document.getElementById("exampleKufiDescription");
                const exampleKufiImageEl = document.getElementById("exampleKufiImage");
                const uniqueKufiHeadingEl = document.getElementById("uniqueKufiHeading");
                const uniqueKufiDescriptionEl = document.getElementById("uniqueKufiDescription");
                const uniqueKufiImageEl = document.getElementById("uniqueKufiImage");

                const exampleKufiHeadingInput = document.getElementById("exampleKufiHeadingInput");
                const exampleKufiDescriptionInput = document.getElementById("exampleKufiDescriptionInput");
                const exampleKufiImageUrlInput = document.getElementById("exampleKufiImageUrlInput");
                const uniqueKufiHeadingInput = document.getElementById("uniqueKufiHeadingInput");
                const uniqueKufiDescriptionInput = document.getElementById("uniqueKufiDescriptionInput");
                const uniqueKufiImageUrlInput = document.getElementById("uniqueKufiImageUrlInput");


                if (docSnap.exists()) {
                    const data = docSnap.data();
                    // Update main title (browser tab title)
                    if (mainTitleEl) mainTitleEl.textContent = data.mainTitle || "Al Jari - High Quality Kufis";
                    if (mainTitleInput) mainTitleInput.value = data.mainTitle || "Al Jari - High Quality Kufis";

                    // Update header title
                    if (headerTitleEl) headerTitleEl.textContent = data.headerTitle || "Al Jari";
                    if (headerTitleInput) headerTitleInput.value = data.headerTitle || "Al Jari";

                    // Update footer text
                    if (footerTextEl) footerTextEl.textContent = data.footerText || "© 2025 Al Jari - All Rights Reserved";
                    if (footerTextInput) footerTextInput.value = data.footerText || "© 2025 Al Jari - All Rights Reserved";

                    // Update background color
                    if (body) body.style.backgroundColor = data.backgroundColor || '#111827';
                    if (backgroundColorInput) backgroundColorInput.value = data.backgroundColor || '#111827';

                    // Update hero image
                    if (heroBg && data.heroImageUrl) heroBg.style.backgroundImage = `url('${data.heroImageUrl}')`;
                    if (heroImageUrlInput) heroImageUrlInput.value = data.heroImageUrl || '';

                    // Update Home Page Hero content
                    if (homeHeroTitleEl) homeHeroTitleEl.textContent = data.homeHeroTitle || "Elegance in Every Stitch";
                    if (homeHeroTitleInput) homeHeroTitleInput.value = data.homeHeroTitle || "";

                    if (homeHeroDescriptionEl) homeHeroDescriptionEl.textContent = data.homeHeroDescription || "Discover our exclusive collection of high-quality Kufis.";
                    if (homeHeroDescriptionInput) homeHeroDescriptionInput.value = data.homeHeroDescription || "";

                    // Update Products Page Heading
                    if (productsPageHeadingEl) productsPageHeadingEl.textContent = data.productsPageHeading || "Our Collection";
                    if (productsPageHeadingInput) productsPageHeadingInput.value = data.productsPageHeading || "";

                    // Update About Page Heading
                    if (aboutPageHeadingEl) aboutPageHeadingEl.textContent = data.aboutPageHeading || "About Al Jari";
                    if (aboutPageHeadingInput) aboutPageHeadingInput.value = data.aboutPageHeading || "";

                    // Update Contact Page Heading
                    if (contactPageHeadingEl) contactPageHeadingEl.textContent = data.contactPageHeading || "Contact Us";
                    if (contactPageHeadingInput) contactPageHeadingInput.value = data.contactPageHeading || "";

                    // Update Fonts
                    if (bodyFontSelect) {
                        body.style.fontFamily = data.bodyFont || 'Poppins, sans-serif';
                        bodyFontSelect.value = data.bodyFont || 'Poppins, sans-serif';
                    }
                    if (headingFontSelect) {
                        // Apply font to all elements with font-playfair class (headings)
                        document.querySelectorAll('.font-playfair').forEach(el => {
                            el.style.fontFamily = data.headingFont || 'Playfair Display, serif';
                        });
                        headingFontSelect.value = data.headingFont || 'Playfair Display, serif';
                    }

                    // Update New Home Page Sections
                    if (exampleKufiHeadingEl) exampleKufiHeadingEl.textContent = data.exampleKufiHeading || "Daily Wear Kufis";
                    if (exampleKufiHeadingInput) exampleKufiHeadingInput.value = data.exampleKufiHeading || "";
                    if (exampleKufiDescriptionEl) exampleKufiDescriptionEl.textContent = data.exampleKufiDescription || "Our collection of comfortable and stylish kufis perfect for everyday use.";
                    if (exampleKufiDescriptionInput) exampleKufiDescriptionInput.value = data.exampleKufiDescription || "";
                    if (exampleKufiImageEl) exampleKufiImageEl.src = data.exampleKufiImageUrl || "https://placehold.co/600x400/374151/FFFFFF?text=Example+Kufi+1";
                    if (exampleKufiImageUrlInput) exampleKufiImageUrlInput.value = data.exampleKufiImageUrl || "";

                    if (uniqueKufiHeadingEl) uniqueKufiHeadingEl.textContent = data.uniqueKufiHeading || "Exclusive Designs";
                    if (uniqueKufiHeadingInput) uniqueKufiHeadingInput.value = data.uniqueKufiHeading || "";
                    if (uniqueKufiDescriptionEl) uniqueKufiDescriptionEl.textContent = data.uniqueKufiDescription || "Explore our limited edition kufis featuring bespoke designs and premium materials.";
                    if (uniqueKufiDescriptionInput) uniqueKufiDescriptionInput.value = data.uniqueKufiDescription || "";
                    if (uniqueKufiImageEl) uniqueKufiImageEl.src = data.uniqueKufiImageUrl || "https://placehold.co/600x400/2D3748/FFFFFF?text=Unique+Kufi+2";
                    if (uniqueKufiImageUrlInput) uniqueKufiImageUrlInput.value = data.uniqueKufiImageUrl || "";

                } else {
                    // Set default values if document doesn't exist
                    if (mainTitleEl) mainTitleEl.textContent = "Al Jari - High Quality Kufis";
                    if (mainTitleInput) mainTitleInput.value = "Al Jari - High Quality Kufis";
                    if (headerTitleEl) headerTitleEl.textContent = "Al Jari";
                    if (headerTitleInput) headerTitleInput.value = "Al Jari";
                    if (footerTextEl) footerTextEl.textContent = "© 2025 Al Jari - All Rights Reserved";
                    if (footerTextInput) footerTextInput.value = "© 2025 Al Jari - All Rights Reserved";
                    if (body) body.style.backgroundColor = '#111827';
                    if (backgroundColorInput) backgroundColorInput.value = '#111827';
                    if (heroBg) heroBg.style.backgroundImage = `url('https://source.unsplash.com/random/1600x900?islamic-pattern')`;
                    if (heroImageUrlInput) heroImageUrlInput.value = '';

                    if (homeHeroTitleEl) homeHeroTitleEl.textContent = "Elegance in Every Stitch";
                    if (homeHeroTitleInput) homeHeroTitleInput.value = "";
                    if (homeHeroDescriptionEl) homeHeroDescriptionEl.textContent = "Discover our exclusive collection of high-quality Kufis.";
                    if (homeHeroDescriptionInput) homeHeroDescriptionInput.value = "";
                    if (productsPageHeadingEl) productsPageHeadingEl.textContent = "Our Collection";
                    if (productsPageHeadingInput) productsPageHeadingInput.value = "";
                    if (aboutPageHeadingEl) aboutPageHeadingEl.textContent = "About Al Jari";
                    if (aboutPageHeadingInput) aboutPageHeadingInput.value = "";
                    if (contactPageHeadingEl) contactPageHeadingEl.textContent = "Contact Us";
                    if (contactPageHeadingInput) contactPageHeadingInput.value = "";
                    
                    if (bodyFontSelect) bodyFontSelect.value = 'Poppins, sans-serif';
                    if (headingFontSelect) headingFontSelect.value = 'Playfair Display, serif';

                    if (exampleKufiHeadingEl) exampleKufiHeadingEl.textContent = "Daily Wear Kufis";
                    if (exampleKufiHeadingInput) exampleKufiHeadingInput.value = "";
                    if (exampleKufiDescriptionEl) exampleKufiDescriptionEl.textContent = "Our collection of comfortable and stylish kufis perfect for everyday use.";
                    if (exampleKufiDescriptionInput) exampleKufiDescriptionInput.value = "";
                    if (exampleKufiImageEl) exampleKufiImageEl.src = "https://placehold.co/600x400/374151/FFFFFF?text=Example+Kufi+1";
                    if (exampleKufiImageUrlInput) exampleKufiImageUrlInput.value = "";

                    if (uniqueKufiHeadingEl) uniqueKufiHeadingEl.textContent = "Exclusive Designs";
                    if (uniqueKufiHeadingInput) uniqueKufiHeadingInput.value = "";
                    if (uniqueKufiDescriptionEl) uniqueKufiDescriptionEl.textContent = "Explore our limited edition kufis featuring bespoke designs and premium materials.";
                    if (uniqueKufiDescriptionInput) uniqueKufiDescriptionInput.value = "";
                    if (uniqueKufiImageEl) uniqueKufiImageEl.src = "https://placehold.co/600x400/2D3748/FFFFFF?text=Unique+Kufi+2";
                    if (uniqueKufiImageUrlInput) uniqueKufiImageUrlInput.value = "";
                }
            }, (error) => {
                console.error("Error fetching global settings:", error);
                showMessage("Error loading website settings.", true);
            });
        }

        // Saves all global settings from the admin panel to Firestore
        window.saveAllSettings = async () => {
            if (!settingsDocRef) {
                showMessage("Firestore is not initialized. Please try again after authentication.", true);
                return;
            }
            try {
                const settingsData = {
                    mainTitle: document.getElementById("mainTitleInput").value,
                    headerTitle: document.getElementById("headerTitleInput").value,
                    footerText: document.getElementById("footerTextInput").value,
                    backgroundColor: document.getElementById("backgroundColorInput").value,
                    heroImageUrl: document.getElementById("heroImageUrlInput").value,
                    homeHeroTitle: document.getElementById("homeHeroTitleInput").value,
                    homeHeroDescription: document.getElementById("homeHeroDescriptionInput").value,
                    productsPageHeading: document.getElementById("productsPageHeadingInput").value,
                    aboutPageHeading: document.getElementById("aboutPageHeadingInput").value,
                    contactPageHeading: document.getElementById("contactPageHeadingInput").value,
                    bodyFont: document.getElementById("bodyFontSelect").value,
                    headingFont: document.getElementById("headingFontSelect").value,
                    // New home page section data
                    exampleKufiHeading: document.getElementById("exampleKufiHeadingInput").value,
                    exampleKufiDescription: document.getElementById("exampleKufiDescriptionInput").value,
                    exampleKufiImageUrl: document.getElementById("exampleKufiImageUrlInput").value,
                    uniqueKufiHeading: document.getElementById("uniqueKufiHeadingInput").value,
                    uniqueKufiDescription: document.getElementById("uniqueKufiDescriptionInput").value,
                    uniqueKufiImageUrl: document.getElementById("uniqueKufiImageUrlInput").value,
                };
                await setDoc(settingsDocRef, settingsData, { merge: true }); // Merge to update specific fields
                showMessage("Website settings saved successfully!");
            } catch (e) {
                console.error("Error saving settings: ", e);
                showMessage("Failed to save website settings.", true);
            }
        };

        // Updates the 'About Us' content in Firestore
        window.editContent = async () => {
            if (!contentDocRef) {
                showMessage("Firestore is not initialized. Please try again after authentication.", true);
                return;
            }
            const newText = document.getElementById("editableText").value;
            try {
                await setDoc(contentDocRef, { aboutText: newText }); // Overwrite or create 'aboutText' field
                showMessage("About Us content updated successfully!");
            } catch (e) {
                console.error("Error updating document: ", e);
                showMessage("Failed to update About Us content.", true);
            }
        };

        // Loads and displays product list from Firestore
        function loadProducts() {
            if (!productsCollectionRef) return; // Exit if Firestore reference is not ready
            onSnapshot(productsCollectionRef, (querySnapshot) => {
                const productListEl = document.getElementById("product-list");
                const noProductsMessage = document.getElementById("no-products-message");
                productListEl.innerHTML = ''; // Clear existing products

                const products = [];
                querySnapshot.forEach((doc) => {
                    products.push({ id: doc.id, ...doc.data() });
                });

                if (products.length === 0) {
                    noProductsMessage.classList.remove('hidden');
                } else {
                    noProductsMessage.classList.add('hidden');
                    products.forEach(product => {
                        displayProduct(product);
                    });
                }
            }, (error) => {
                console.error("Error fetching products:", error);
                showMessage("Error loading products.", true);
            });
        }

        // Displays a single product card in the products list
        function displayProduct(product) {
            const productListEl = document.getElementById("product-list");
            const productCard = document.createElement("div");
            productCard.id = `product-${product.id}`;
            productCard.className = `product-card bg-gray-800 rounded-xl shadow-lg overflow-hidden relative flex flex-col transform transition-transform duration-200 hover:scale-105`;

            // Default image if none provided or invalid
            const imageUrl = product.imageUrl || `https://placehold.co/400x300/374151/FFFFFF?text=No+Image`;

            // Check if admin panel is currently visible to determine initial state of controls
            const isAdminPanelVisible = !document.getElementById("adminPanel").classList.contains('hidden');
            const adminControlsClass = isAdminPanelVisible ? '' : 'hidden'; // Hide if admin panel is hidden

            productCard.innerHTML = `
                <img src="${imageUrl}" alt="${product.name}" class="w-full h-48 object-cover transition-transform duration-300 transform hover:scale-110" onerror="this.onerror=null;this.src='https://placehold.co/400x300/374151/FFFFFF?text=Image+Load+Error';">
                <div class="p-5 flex-grow">
                    <h3 class="text-xl font-semibold text-white mb-2 font-poppins">${product.name}</h3>
                    <p class="text-gray-400 text-sm font-inter">${product.description}</p>
                    ${product.sizes && product.sizes.length > 0 ? `
                        <p class="text-gray-300 text-sm mt-2 font-inter">Sizes: ${product.sizes.join(', ')}</p>
                    ` : ''}
                    <div class="flex items-center justify-between mt-4">
                        <span class="text-2xl font-bold text-indigo-400 font-playfair">$${product.price ? product.price.toFixed(2) : '0.00'}</span>
                        <button class="bg-indigo-600 text-white px-4 py-2 rounded-lg hover:bg-indigo-700 transition-colors font-poppins">Add to Cart</button>
                    </div>
                </div>
                <div class="admin-controls absolute top-2 right-2 space-x-2 ${adminControlsClass}">
                    <button onclick="editProduct('${product.id}')" class="bg-blue-500 text-white p-2 rounded-full shadow-md hover:bg-blue-600 transition-colors">
                        <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M13.586 3.586a2 2 0 112.828 2.828l-.793.793-2.828-2.828.793-.793zm-5.657 5.657l-1.414 1.414L.929 18.09a1 1 0 00.322 1.402 1 1 0 001.402.322l7.07-7.071-1.414-1.414z"></path></svg>
                    </button>
                    <button onclick="deleteProduct('${product.id}')" class="bg-red-500 text-white p-2 rounded-full shadow-md hover:bg-red-600 transition-colors">
                        <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 011-1h4a1 1 0 110 2H8a1 1 0 01-1-1zm6 3a1 1 0 100 2H8a1 1 0 100-2h5z" clip-rule="evenodd"></path></svg>
                    </button>
                </div>
            `;
            productListEl.appendChild(productCard);
        }

        // Handles adding a new product or updating an existing one
        window.handleAddOrUpdateProduct = async () => {
            if (!productsCollectionRef) {
                showMessage("Firestore is not initialized. Please try again after authentication.", true);
                return;
            }
            const name = document.getElementById("productName").value.trim();
            const imageUrl = document.getElementById("productImageUrl").value.trim();
            const description = document.getElementById("productDescription").value.trim();
            const sizesInput = document.getElementById("productSizes").value.trim();
            const price = parseFloat(document.getElementById("productPrice").value);

            if (!name || !description || isNaN(price)) {
                showMessage("Please fill in all product fields (Name, Description, Price).", true);
                return;
            }
            if (price < 0) {
                showMessage("Price cannot be negative.", true);
                return;
            }

            const sizes = sizesInput ? sizesInput.split(',').map(s => s.trim()).filter(s => s !== '') : [];

            const productData = { name, imageUrl, description, sizes, price };

            try {
                if (productToEditId) {
                    // Update existing product
                    const productDoc = doc(db, 'artifacts', typeof __app_id !== 'undefined' ? __app_id : 'al-jari-website-default', 'public', 'data', 'products', productToEditId);
                    await updateDoc(productDoc, productData);
                    showMessage("Product updated successfully!");
                } else {
                    // Add new product
                    await addDoc(productsCollectionRef, productData);
                    showMessage("Product added successfully!");
                }
                clearProductForm(); // Clear the form after successful operation
            } catch (e) {
                console.error("Error adding/updating product: ", e);
                showMessage(`Failed to ${productToEditId ? 'update' : 'add'} product.`, true);
            }
        };

        // Populates the form for editing an existing product
        window.editProduct = (id) => {
            const productElement = document.getElementById(`product-${id}`);
            if (productElement) {
                const name = productElement.querySelector('h3').textContent;
                const description = productElement.querySelector('.text-gray-400').textContent;
                const price = parseFloat(productElement.querySelector('.text-indigo-400').textContent.replace('$', ''));
                const imageUrl = productElement.querySelector('img').src;
                const sizesText = productElement.querySelector('.text-gray-300') ? productElement.querySelector('.text-gray-300').textContent.replace('Sizes: ', '') : '';

                document.getElementById("productName").value = name;
                document.getElementById("productImageUrl").value = imageUrl.startsWith('https://placehold.co/') ? '' : imageUrl; // Clear placeholder image URL if it's the default
                document.getElementById("productDescription").value = description;
                document.getElementById("productSizes").value = sizesText;
                document.getElementById("productPrice").value = price;

                document.getElementById("addProductButton").textContent = "Update Product";
                document.getElementById("productFormHeading").textContent = "Edit Product:";
                document.getElementById("cancelProductEditButton").classList.remove('hidden');
                productToEditId = id; // Store the ID of the product being edited
            } else {
                showMessage("Product not found for editing.", true);
            }
        };

        // Clears the product form and resets it to "Add Product" mode
        function clearProductForm() {
            document.getElementById("productName").value = "";
            document.getElementById("productImageUrl").value = "";
            document.getElementById("productDescription").value = "";
            document.getElementById("productSizes").value = "";
            document.getElementById("productPrice").value = "";
            document.getElementById("addProductButton").textContent = "Add Product";
            document.getElementById("productFormHeading").textContent = "Add New Product:";
            document.getElementById("cancelProductEditButton").classList.add('hidden');
            productToEditId = null; // Clear the edit ID
        }

        // Resets the product form without saving
        window.cancelProductEdit = () => {
            clearProductForm();
        };

        // Prepares for product deletion by showing confirmation modal
        window.deleteProduct = (id) => {
            showConfirmationModal("Are you sure you want to delete this product?", async () => {
                try {
                    const productDoc = doc(db, 'artifacts', typeof __app_id !== 'undefined' ? __app_id : 'al-jari-website-default', 'public', 'data', 'products', id);
                    await deleteDoc(productDoc);
                    showMessage("Product deleted successfully!");
                } catch (e) {
                    console.error("Error deleting product: ", e);
                    showMessage("Failed to delete product.", true);
                }
            });
        };
    </script>
</body>
</html>
