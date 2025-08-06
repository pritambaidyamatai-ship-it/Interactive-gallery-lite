<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Image Gallery</title>
    <style>
        :root {
            --primary-color: #4a6fa5;
            --secondary-color: #166088;
            --accent-color: #4fc3fc;
            --light-color: #dbe9ee;
            --dark-color: #1a1a1a;
            --transition-speed: 0.3s;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f0f0f0;
            color: var(--dark-color);
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
        }

        header {
            text-align: center;
            margin-bottom: 2rem;
        }

        h1 {
            color: var(--secondary-color);
            margin-bottom: 1rem;
        }

        .filter-controls {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 0.5rem;
            margin-bottom: 1.5rem;
        }

        .filter-btn {
            padding: 0.5rem 1rem;
            border: none;
            background-color: var(--light-color);
            color: var(--dark-color);
            border-radius: 20px;
            cursor: pointer;
            transition: all var(--transition-speed) ease;
        }

        .filter-btn:hover, .filter-btn.active {
            background-color: var(--primary-color);
            color: white;
        }

        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 1.5rem;
        }

        .gallery-item {
            position: relative;
            overflow: hidden;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            transition: all var(--transition-speed) ease;
        }

        .gallery-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
        }

        .gallery-img {
            width: 100%;
            height: 200px;
            object-fit: cover;
            display: block;
            transition: transform var(--transition-speed) ease;
        }

        .gallery-item:hover .gallery-img {
            transform: scale(1.05);
        }

        .caption {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background-color: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 1rem;
            transform: translateY(100%);
            transition: transform var(--transition-speed) ease;
        }

        .gallery-item:hover .caption {
            transform: translateY(0);
        }

        /* Lightbox Styles */
        .lightbox {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.9);
            z-index: 1000;
            opacity: 0;
            transition: opacity var(--transition-speed) ease;
        }

        .lightbox.active {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            opacity: 1;
        }

        .lightbox-img {
            max-width: 90%;
            max-height: 80vh;
            object-fit: contain;
            margin-bottom: 1rem;
        }

        .lightbox-caption {
            color: white;
            text-align: center;
            max-width: 80%;
        }

        .lightbox-nav {
            position: absolute;
            top: 50%;
            width: 100%;
            display: flex;
            justify-content: space-between;
            transform: translateY(-50%);
            padding: 0 2rem;
        }

        .nav-btn {
            background-color: rgba(255, 255, 255, 0.2);
            color: white;
            border: none;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            font-size: 1.5rem;
            cursor: pointer;
            transition: all var(--transition-speed) ease;
        }

        .nav-btn:hover {
            background-color: rgba(255, 255, 255, 0.5);
        }

        .close-btn {
            position: absolute;
            top: 2rem;
            right: 2rem;
            background-color: transparent;
            color: white;
            border: none;
            font-size: 2rem;
            cursor: pointer;
        }

        /* Responsive Adjustments */
        @media (max-width: 768px) {
            .gallery {
                grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
                gap: 1rem;
            }
            
            .lightbox-img {
                max-width: 95%;
                max-height: 60vh;
            }
        }

        @media (max-width: 480px) {
            .gallery {
                grid-template-columns: 1fr;
            }
            
            .lightbox-nav {
                padding: 0 1rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Interactive Image Gallery</h1>
            <p>Browse our collection of stunning images</p>
        </header>

        <div class="filter-controls">
            <button class="filter-btn active" data-filter="all">All</button>
            <button class="filter-btn" data-filter="nature">Nature</button>
            <button class="filter-btn" data-filter="city">City</button>
            <button class="filter-btn" data-filter="people">People</button>
            <button class="filter-btn" data-filter="food">Food</button>
        </div>

        <div class="gallery">
            <!-- Nature Category -->
            <div class="gallery-item" data-category="nature">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/8e13fb87-f85b-4f6b-95f5-4852b886fdff.png" alt="Majestic mountain landscape at sunrise with mist in the valleys" class="gallery-img">
                <div class="caption">
                    <h3>Mountain Sunrise</h3>
                    <p>Beautiful mountain landscape during golden hour</p>
                </div>
            </div>

            <div class="gallery-item" data-category="nature">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/fdd3e5cd-dd9e-4670-8ca5-24fbecba20ca.png" alt="Tropical waterfall cascading into a crystal clear blue pool surrounded by lush greenery" class="gallery-img">
                <div class="caption">
                    <h3>Tropical Waterfall</h3>
                    <p>Refreshing waterfall in a rainforest</p>
                </div>
            </div>

            <div class="gallery-item" data-category="nature">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/25a0f69f-81be-4aa0-99ec-d872cfe3ceda.png" alt="Colorful coral reef with diverse marine life and schooling fish in turquoise water" class="gallery-img">
                <div class="caption">
                    <h3>Coral Reef</h3>
                    <p>Vibrant underwater ecosystem</p>
                </div>
            </div>

            <!-- City Category -->
            <div class="gallery-item" data-category="city">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/993f4ad8-920f-4ca2-9bc5-b9fc3d10cf6b.png" alt="Nighttime cityscape with illuminated skyscrapers and neon lights reflecting on wet streets" class="gallery-img">
                <div class="caption">
                    <h3>Urban Nightscape</h3>
                    <p>City lights after rain</p>
                </div>
            </div>

            <div class="gallery-item" data-category="city">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/08badd3a-4f44-4e81-8e91-32e72d251f3b.png" alt="Aerial view of a modern metropolis with geometric building patterns and bridges" class="gallery-img">
                <div class="caption">
                    <h3>Skyline View</h3>
                    <p>Birds eye perspective</p>
                </div>
            </div>

            <div class="gallery-item" data-category="city">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/6d8e0c82-c031-4d14-b629-c529e487bda2.png" alt="Historic European street lined with colorful buildings and outdoor cafes" class="gallery-img">
                <div class="caption">
                    <h3>Old Town Charm</h3>
                    <p>Quaint historic district</p>
                </div>
            </div>

            <!-- People Category -->
            <div class="gallery-item" data-category="people">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/7e6b2f43-b4ab-4cc8-8335-7df6d704aaa6.png" alt="Portrait of an elderly woman with deep wrinkles and wise expression, soft natural lighting" class="gallery-img">
                <div class="caption">
                    <h3>Wisdom</h3>
                    <p>Character portrait</p>
                </div>
            </div>

            <div class="gallery-item" data-category="people">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/b55bf603-fc0c-4160-b721-a61d3d54ff3f.png" alt="Silhouette of a dancer mid-performance against a dramatic sunset background" class="gallery-img">
                <div class="caption">
                    <h3>Graceful Motion</h3>
                    <p>Capturing movement</p>
                </div>
            </div>

            <div class="gallery-item" data-category="people">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/9d55132b-9ae9-45f4-afcd-9b4a4995b53d.png" alt="Candid shot of children laughing and playing in a park with sunlight filtering through trees" class="gallery-img">
                <div class="caption">
                    <h3>Childhood Joy</h3>
                    <p>Spontaneous moment</p>
                </div>
            </div>

            <!-- Food Category -->
            <div class="gallery-item" data-category="food">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/18dfcef3-367c-4330-95d5-a3f7bf70fe40.png" alt="Artisanal pizza with fresh ingredients on a wooden cutting board, overhead shot" class="gallery-img">
                <div class="caption">
                    <h3>Gourmet Pizza</h3>
                    <p>Homemade with love</p>
                </div>
            </div>

            <div class="gallery-item" data-category="food">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/91255885-6e23-4b9d-8cbb-4db20c4096dd.png" alt="Colorful sushi platter arranged artistically with wasabi and ginger on a black slate" class="gallery-img">
                <div class="caption">
                    <h3>Sushi Selection</h3>
                    <p>Fresh and delicious</p>
                </div>
            </div>

            <div class="gallery-item" data-category="food">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/a41a8074-8e5c-4d4b-aad6-542b26892d2d.png" alt="Stack of fluffy pancakes with fresh berries and maple syrup drizzle on rustic table" class="gallery-img">
                <div class="caption">
                    <h3>Breakfast Delight</h3>
                    <p>Breakfast perfection</p>
                </div>
            </div>
        </div>
    </div>

    <!-- Lightbox -->
    <div class="lightbox">
        <button class="close-btn">&times;</button>
        <img src="" alt="" class="lightbox-img">
        <div class="lightbox-caption">
            <h3></h3>
            <p></p>
        </div>
        <div class="lightbox-nav">
            <button class="nav-btn prev-btn"><</button>
            <button class="nav-btn next-btn">></button>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Lightbox functionality
            const galleryItems = document.querySelectorAll('.gallery-item');
            const lightbox = document.querySelector('.lightbox');
            const lightboxImg = document.querySelector('.lightbox-img');
            const lightboxCaptionTitle = document.querySelector('.lightbox-caption h3');
            const lightboxCaptionDesc = document.querySelector('.lightbox-caption p');
            const closeBtn = document.querySelector('.close-btn');
            const prevBtn = document.querySelector('.prev-btn');
            const nextBtn = document.querySelector('.next-btn');
            
            let currentImageIndex = 0;
            const images = Array.from(galleryItems);
            
            // Open lightbox with clicked image
            galleryItems.forEach((item, index) => {
                item.addEventListener('click', () => {
                    currentImageIndex = index;
                    updateLightbox();
                    lightbox.classList.add('active');
                    document.body.style.overflow = 'hidden';
                });
            });
            
            // Update lightbox content
            function updateLightbox() {
                const activeImg = images[currentImageIndex].querySelector('.gallery-img');
                const activeCaption = images[currentImageIndex].querySelector('.caption');
                
                lightboxImg.src = activeImg.src;
                lightboxImg.alt = activeImg.alt;
                lightboxCaptionTitle.textContent = activeCaption.querySelector('h3').textContent;
                lightboxCaptionDesc.textContent = activeCaption.querySelector('p').textContent;
            }
            
            // Navigation
            prevBtn.addEventListener('click', (e) => {
                e.stopPropagation();
                currentImageIndex = (currentImageIndex - 1 + images.length) % images.length;
                updateLightbox();
            });
            
            nextBtn.addEventListener('click', (e) => {
                e.stopPropagation();
                currentImageIndex = (currentImageIndex + 1) % images.length;
                updateLightbox();
            });
            
            // Close lightbox
            closeBtn.addEventListener('click', () => {
                lightbox.classList.remove('active');
                document.body.style.overflow = 'auto';
            });
            
            // Close when clicking outside
            lightbox.addEventListener('click', (e) => {
                if (e.target === lightbox) {
                    lightbox.classList.remove('active');
                    document.body.style.overflow = 'auto';
                }
            });
            
            // Keyboard navigation
            document.addEventListener('keydown', (e) => {
                if (!lightbox.classList.contains('active')) return;
                
                if (e.key === 'Escape') {
                    lightbox.classList.remove('active');
                    document.body.style.overflow = 'auto';
                } else if (e.key === 'ArrowLeft') {
                    currentImageIndex = (currentImageIndex - 1 + images.length) % images.length;
                    updateLightbox();
                } else if (e.key === 'ArrowRight') {
                    currentImageIndex = (currentImageIndex + 1) % images.length;
                    updateLightbox();
                }
            });

            // Filter functionality
            const filterButtons = document.querySelectorAll('.filter-btn');
            
            filterButtons.forEach(button => {
                button.addEventListener('click', () => {
                    // Set active button
                    filterButtons.forEach(btn => btn.classList.remove('active'));
                    button.classList.add('active');
                    
                    const filterValue = button.dataset.filter;
                    
                    // Filter images
                    galleryItems.forEach(item => {
                        if (filterValue === 'all' || item.dataset.category === filterValue) {
                            item.style.display = 'block';
                            item.style.animation = 'fadeIn 0.5s';
                        } else {
                            item.style.display = 'none';
                        }
                    });
                });
            });

            // Animation for filtered items
            const style = document.createElement('style');
            style.textContent = `
                @keyframes fadeIn {
                    from { opacity: 0; transform: scale(0.95); }
                    to { opacity: 1; transform: scale(1); }
                }
            `;
            document.head.appendChild(style);
        });
    </script>
</body>
</html>

