<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DailyToolBox - 100+ Free Online Tools</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #4361ee;
            --dark: #212529;
            --light: #f8f9fa;
            --gray: #6c757d;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            transition: all 0.3s ease;
        }
        
        body {
            background-color: var(--light);
            color: var(--dark);
        }
        
        body.dark-mode {
            background-color: #121212;
            color: #f5f5f5;
        }
        
        /* Header Styles */
        header {
            background-color: var(--primary);
            color: white;
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        .logo {
            font-size: 1.8rem;
            font-weight: bold;
            display: flex;
            align-items: center;
        }
        
        .logo i {
            margin-right: 10px;
        }
        
        /* Navigation */
        nav {
            display: flex;
            gap: 1.5rem;
        }
        
        nav a {
            color: white;
            text-decoration: none;
            font-weight: 500;
        }
        
        /* Main Content */
        .container {
            max-width: 1200px;
            margin: 2rem auto;
            padding: 0 1rem;
        }
        
        .search-container {
            margin: 2rem 0;
            position: relative;
        }
        
        #searchInput {
            width: 100%;
            padding: 12px 20px;
            border: 2px solid #ddd;
            border-radius: 50px;
            font-size: 1rem;
        }
        
        /* Tool Categories Grid */
        .categories-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1.5rem;
            margin-top: 2rem;
        }
        
        .category-card {
            background: white;
            border-radius: 10px;
            padding: 1.5rem;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            cursor: pointer;
        }
        
        .dark-mode .category-card {
            background: #1e1e1e;
            box-shadow: 0 4px 6px rgba(0,0,0,0.3);
        }
        
        .category-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }
        
        .category-title {
            font-size: 1.3rem;
            margin-bottom: 1rem;
            color: var(--primary);
            display: flex;
            align-items: center;
        }
        
        .category-title i {
            margin-right: 10px;
            font-size: 1.5rem;
        }
        
        .tools-list {
            list-style-type: none;
        }
        
        .tools-list li {
            padding: 8px 0;
            border-bottom: 1px solid #eee;
        }
        
        .dark-mode .tools-list li {
            border-bottom: 1px solid #333;
        }
        
        .tools-list li:last-child {
            border-bottom: none;
        }
        
        .tools-list a {
            color: var(--gray);
            text-decoration: none;
            display: flex;
            align-items: center;
        }
        
        .dark-mode .tools-list a {
            color: #aaa;
        }
        
        .tools-list a:hover {
            color: var(--primary);
        }
        
        .tools-list i {
            margin-right: 8px;
            font-size: 0.9rem;
        }
        
        /* Footer */
        footer {
            background-color: var(--dark);
            color: white;
            padding: 2rem;
            text-align: center;
            margin-top: 3rem;
        }
        
        .footer-links {
            display: flex;
            justify-content: center;
            gap: 2rem;
            margin: 1rem 0;
        }
        
        .footer-links a {
            color: white;
            text-decoration: none;
        }
        
        /* Dark Mode Toggle */
        .dark-mode-toggle {
            background: none;
            border: none;
            color: white;
            font-size: 1.2rem;
            cursor: pointer;
        }
        
        /* Responsive Design */
        @media (max-width: 768px) {
            header {
                flex-direction: column;
                padding: 1rem;
            }
            
            .logo {
                margin-bottom: 1rem;
            }
            
            nav {
                flex-wrap: wrap;
                justify-content: center;
            }
            
            .categories-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="logo">
            <i class="fas fa-toolbox"></i>
            <span>DailyToolBox</span>
        </div>
        <nav>
            <a href="#">Home</a>
            <a href="#">All Tools</a>
            <a href="#">Categories</a>
            <a href="#">Contact</a>
        </nav>
        <button class="dark-mode-toggle" id="darkModeToggle">
            <i class="fas fa-moon"></i>
        </button>
    </header>
    
    <div class="container">
        <h1>100+ Free Online Tools for Daily Use</h1>
        <p>All-in-one solution for your PDF, image, video, text and other conversion needs</p>
        
        <div class="search-container">
            <input type="text" id="searchInput" placeholder="Search for any tool...">
        </div>
        
        <div class="categories-grid" id="categoriesGrid">
            <!-- PDF Tools -->
            <div class="category-card" onclick="location.href='pdf-tools.html'">
                <h2 class="category-title"><i class="fas fa-file-pdf"></i> PDF Tools</h2>
                <ul class="tools-list">
                    <li><a href="pdf-to-word.html"><i class="fas fa-arrow-right"></i> PDF to Word</a></li>
                    <li><a href="word-to-pdf.html"><i class="fas fa-arrow-right"></i> Word to PDF</a></li>
                    <li><a href="pdf-compressor.html"><i class="fas fa-arrow-right"></i> PDF Compressor</a></li>
                    <li><a href="merge-pdf.html"><i class="fas fa-arrow-right"></i> Merge PDF</a></li>
                    <li><a href="split-pdf.html"><i class="fas fa-arrow-right"></i> Split PDF</a></li>
                </ul>
            </div>
            
            <!-- Image Tools -->
            <div class="category-card" onclick="location.href='image-tools.html'">
                <h2 class="category-title"><i class="fas fa-image"></i> Image Tools</h2>
                <ul class="tools-list">
                    <li><a href="image-resizer.html"><i class="fas fa-arrow-right"></i> Image Resizer</a></li>
                    <li><a href="jpg-to-png.html"><i class="fas fa-arrow-right"></i> JPG to PNG</a></li>
                    <li><a href="image-compressor.html"><i class="fas fa-arrow-right"></i> Image Compressor</a></li>
                    <li><a href="background-remover.html"><i class="fas fa-arrow-right"></i> Background Remover</a></li>
                    <li><a href="webp-converter.html"><i class="fas fa-arrow-right"></i> WebP Converter</a></li>
                </ul>
            </div>
            
            <!-- Video & Audio Tools -->
            <div class="category-card" onclick="location.href='video-tools.html'">
                <h2 class="category-title"><i class="fas fa-video"></i> Video & Audio Tools</h2>
                <ul class="tools-list">
                    <li><a href="youtube-downloader.html"><i class="fas fa-arrow-right"></i> YouTube Downloader</a></li>
                    <li><a href="mp4-to-mp3.html"><i class="fas fa-arrow-right"></i> MP4 to MP3</a></li>
                    <li><a href="video-compressor.html"><i class="fas fa-arrow-right"></i> Video Compressor</a></li>
                    <li><a href="audio-cutter.html"><i class="fas fa-arrow-right"></i> Audio Cutter</a></li>
                </ul>
            </div>
            
            <!-- Text & AI Tools -->
            <div class="category-card" onclick="location.href='text-tools.html'">
                <h2 class="category-title"><i class="fas fa-keyboard"></i> Text & AI Tools</h2>
                <ul class="tools-list">
                    <li><a href="paraphraser.html"><i class="fas fa-arrow-right"></i> Paraphraser</a></li>
                    <li><a href="grammar-checker.html"><i class="fas fa-arrow-right"></i> Grammar Checker</a></li>
                    <li><a href="text-summarizer.html"><i class="fas fa-arrow-right"></i> Text Summarizer</a></li>
                    <li><a href="text-to-speech.html"><i class="fas fa-arrow-right"></i> Text to Speech</a></li>
                </ul>
            </div>
            
            <!-- Developer Tools -->
            <div class="category-card" onclick="location.href='developer-tools.html'">
                <h2 class="category-title"><i class="fas fa-code"></i> Developer Tools</h2>
                <ul class="tools-list">
                    <li><a href="json-formatter.html"><i class="fas fa-arrow-right"></i> JSON Formatter</a></li>
                    <li><a href="regex-tester.html"><i class="fas fa-arrow-right"></i> Regex Tester</a></li>
                    <li><a href="html-formatter.html"><i class="fas fa-arrow-right"></i> HTML Formatter</a></li>
                    <li><a href="base64-converter.html"><i class="fas fa-arrow-right"></i> Base64 Converter</a></li>
                </ul>
            </div>
            
            <!-- SEO Tools -->
            <div class="category-card" onclick="location.href='seo-tools.html'">
                <h2 class="category-title"><i class="fas fa-search"></i> SEO Tools</h2>
                <ul class="tools-list">
                    <li><a href="keyword-extractor.html"><i class="fas fa-arrow-right"></i> Keyword Extractor</a></li>
                    <li><a href="meta-tag-generator.html"><i class="fas fa-arrow-right"></i> Meta Tag Generator</a></li>
                    <li><a href="plagiarism-checker.html"><i class="fas fa-arrow-right"></i> Plagiarism Checker</a></li>
                    <li><a href="title-generator.html"><i class="fas fa-arrow-right"></i> Title Generator</a></li>
                </ul>
            </div>
            
            <!-- Converter & Calculators -->
            <div class="category-card" onclick="location.href='converter-tools.html'">
                <h2 class="category-title"><i class="fas fa-calculator"></i> Converters & Calculators</h2>
                <ul class="tools-list">
                    <li><a href="currency-converter.html"><i class="fas fa-arrow-right"></i> Currency Converter</a></li>
                    <li><a href="unit-converter.html"><i class="fas fa-arrow-right"></i> Unit Converter</a></li>
                    <li><a href="age-calculator.html"><i class="fas fa-arrow-right"></i> Age Calculator</a></li>
                    <li><a href="bmi-calculator.html"><i class="fas fa-arrow-right"></i> BMI Calculator</a></li>
                </ul>
            </div>
            
            <!-- Miscellaneous Tools -->
            <div class="category-card" onclick="location.href='misc-tools.html'">
                <h2 class="category-title"><i class="fas fa-random"></i> Miscellaneous Tools</h2>
                <ul class="tools-list">
                    <li><a href="qr-generator.html"><i class="fas fa-arrow-right"></i> QR Code Generator</a></li>
                    <li><a href="password-generator.html"><i class="fas fa-arrow-right"></i> Password Generator</a></li>
                    <li><a href="world-clock.html"><i class="fas fa-arrow-right"></i> World Clock</a></li>
                    <li><a href="speed-test.html"><i class="fas fa-arrow-right"></i> Internet Speed Test</a></li>
                </ul>
            </div>
        </div>
    </div>
    
    <footer>
        <p>© 2023 DailyToolBox. All rights reserved.</p>
        <div class="footer-links">
            <a href="#">Privacy Policy</a>
            <a href="#">Terms of Service</a>
            <a href="#">Contact Us</a>
            <a href="#">Feedback</a>
        </div>
        <p>Made with <i class="fas fa-heart" style="color:red"></i> for everyone</p>
    </footer>

    <script>
        // Dark Mode Toggle
        const darkModeToggle = document.getElementById('darkModeToggle');
        const body = document.body;
        
        // Check for saved user preference
        if (localStorage.getItem('darkMode') === 'enabled') {
            body.classList.add('dark-mode');
            darkModeToggle.innerHTML = '<i class="fas fa-sun"></i>';
        }
        
        darkModeToggle.addEventListener('click', () => {
            body.classList.toggle('dark-mode');
            
            if (body.classList.contains('dark-mode')) {
                localStorage.setItem('darkMode', 'enabled');
                darkModeToggle.innerHTML = '<i class="fas fa-sun"></i>';
            } else {
                localStorage.setItem('darkMode', 'disabled');
                darkModeToggle.innerHTML = '<i class="fas fa-moon"></i>';
            }
        });
        
        // Search Functionality
        const searchInput = document.getElementById('searchInput');
        const categoryCards = document.querySelectorAll('.category-card');
        
        searchInput.addEventListener('input', () => {
            const searchTerm = searchInput.value.toLowerCase();
            
            categoryCards.forEach(card => {
                const title = card.querySelector('.category-title').textContent.toLowerCase();
                const tools = card.querySelectorAll('.tools-list a');
                let hasMatch = false;
                
                // Check if title matches
                if (title.includes(searchTerm)) {
                    hasMatch = true;
                }
                
                // Check if any tool matches
                tools.forEach(tool => {
                    const toolText = tool.textContent.toLowerCase();
                    if (toolText.includes(searchTerm)) {
                        hasMatch = true;
                        tool.style.fontWeight = 'bold';
                        tool.style.color = 'var(--primary)';
                    } else {
                        tool.style.fontWeight = 'normal';
                        tool.style.color = '';
                    }
                });
                
                // Show/hide category based on match
                card.style.display = hasMatch ? 'block' : 'none';
            });
        });
        
        // Make entire category card clickable
        categoryCards.forEach(card => {
            card.style.cursor = 'pointer';
        });
    </script>
</body>
</html>
