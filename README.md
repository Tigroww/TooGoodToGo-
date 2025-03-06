    # TooGoodToGo-
    <!DOCTYPE html>
    <html lang="fr">
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Slide Button</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f7f7f7;
        }

        .slider-container {
            width: 300px;
            height: 60px;
            background: white;
            border-radius: 30px;
            box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
            position: relative;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 16px;
            font-weight: bold;
            color: black;
        }

        .slider-button {
            width: 60px;
            height: 60px;
            background: teal;
            border-radius: 50%;
            position: absolute;
            left: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: grab;
            transition: left 0.2s ease;
        }

        .slider-button:active {
            cursor: grabbing;
        }

        .arrow {
            color: white;
            font-size: 24px;
        }
    </style>
    </head>
    <body>

    <div class="slider-container" id="sliderContainer">
        Valider pour collecter
        <div class="slider-button" id="sliderButton">
            <span class="arrow">➡️</span>
        </div>
    </div>

    <script>
        const sliderButton = document.getElementById("sliderButton");
        const sliderContainer = document.getElementById("sliderContainer");
        let isDragging = false;

        sliderButton.addEventListener("mousedown", (e) => {
            isDragging = true;
            document.addEventListener("mousemove", onMouseMove);
            document.addEventListener("mouseup", onMouseUp);
        });

        function onMouseMove(e) {
            if (!isDragging) return;
            
            let containerRect = sliderContainer.getBoundingClientRect();
            let buttonRect = sliderButton.getBoundingClientRect();
            let offsetX = e.clientX - containerRect.left - (buttonRect.width / 2);

            if (offsetX < 0) offsetX = 0;
            if (offsetX > containerRect.width - buttonRect.width) offsetX = containerRect.width - buttonRect.width;

            sliderButton.style.left = offsetX + "px";

            if (offsetX >= containerRect.width - buttonRect.width) {
                sliderContainer.innerText = "Collecté !";
                sliderButton.style.display = "none";
            }
        }

        function onMouseUp() {
            isDragging = false;
            document.removeEventListener("mousemove", onMouseMove);
            document.removeEventListener("mouseup", onMouseUp);
            
            if (sliderButton.style.left !== "240px") { // Si pas validé, retour à 0
                sliderButton.style.left = "0px";
            }
        }
    </script>

    </body>
    </html>
