---
title: Resume
permalink: /resume/
weight: 20
---


<!-- <object data="/assets/Quentin_CAUDRON.pdf" width="1000" height="1000" type='application/pdf'></object> -->



<style>
    
    /* Make sure body respects header/footer */
    body {
        background-color: #f4f4f4;
        margin: 0;
        padding: 0;
        font-family: Arial, sans-serif;
    }

    /* Toolbar styling */
    #pdf-toolbar {
        display: flex;
        justify-content: center;
        gap: 10px;
        padding: 10px;
        background: #333;
        color: white;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        z-index: 1000;
    }

    #pdf-toolbar button {
        background: #555;
        color: white;
        border: none;
        padding: 8px 12px;
        cursor: pointer;
        font-size: 14px;
        border-radius: 4px;
    }

    #pdf-toolbar button:hover {
        background: #777;
    }

    /* Wrapper ensures it doesn’t overlap */
    #pdf-container {
        display: flex;
        justify-content: center;
        align-items: flex-start;
        margin-top: 100px; /* Adjust based on header height */
        padding-bottom: 50px; /* Adjust based on footer */
    }

    #pdf-viewer {
        width: 100%;
        max-width: 1200px;
        background: white;
        box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
        padding: 20px;
        border-radius: 8px;
        text-align: center;
    }

    canvas {
        display: block;
        margin: 10px auto;
        max-width: 100%;
        height: auto;
    }
</style>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.14.305/pdf.min.js"></script>

<!-- Toolbar -->
<div id="pdf-toolbar">
    <button id="zoomOut">➖ Zoom Out</button>
    <button id="zoomIn">➕ Zoom In</button>
    <button id="downloadPdf">⬇ Download</button>
</div>

<div id="pdf-container">
    <div id="pdf-viewer"></div>
</div>


<script>
    document.addEventListener("DOMContentLoaded", function () {
        var url = "/assets/Quentin_CAUDRON.pdf";
        var loadingTask = pdfjsLib.getDocument(url);
        var pdfDoc = null;
        var pageNum = 1;
        var scale = 1.5;
        var viewer = document.getElementById("pdf-viewer");

        function renderPage(num) {
            pdfDoc.getPage(num).then(function (page) {
                var viewport = page.getViewport({ scale: scale });

                var canvas = document.createElement("canvas");
                var context = canvas.getContext("2d");
                canvas.width = viewport.width;
                canvas.height = viewport.height;

                viewer.innerHTML = ""; // Clear previous page
                viewer.appendChild(canvas);

                var renderContext = { canvasContext: context, viewport: viewport };
                page.render(renderContext);
            });
        }

        loadingTask.promise.then(function (pdf) {
            pdfDoc = pdf;
            renderPage(pageNum);
        });

        // Toolbar button actions
        document.getElementById("zoomIn").addEventListener("click", function () {
            scale += 0.2;
            renderPage(pageNum);
        });

        document.getElementById("zoomOut").addEventListener("click", function () {
            if (scale > 0.5) {
                scale -= 0.2;
                renderPage(pageNum);
            }
        });
        document.getElementById("downloadPdf").addEventListener("click", function () {
            window.open(url, "_blank");
        });
    });
</script>