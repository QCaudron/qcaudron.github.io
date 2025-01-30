---
title: Resume
permalink: /resume/
weight: 20
---


<style>
    /* General Styles */
    body {
        background-color: #f4f4f4;
        margin: 0;
        padding: 0;
        font-family: Arial, sans-serif;
    }

    /* Keep toolbar inside content */
    #pdf-wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 20px;
    }

    /* Toolbar inside content, not floating */
    #pdf-toolbar {
        display: flex;
        justify-content: center;
        gap: 10px;
        padding: 10px;
        background: #333;
        color: white;
        width: 120%;
        max-width: 1200px;
        border-radius: 8px;
        margin-bottom: 10px;
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

    /* PDF Viewer */
    #pdf-container {
        width: 120%;
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

<!-- Wrapper to ensure it stays inside the content area -->
<div id="pdf-wrapper">
    <div id="pdf-toolbar">
        <button id="zoomOut">➖ Zoom Out</button>
        <button id="zoomIn">➕ Zoom In</button>
        <button id="downloadPdf">⬇ Download</button>
    </div>
    <div id="pdf-container"></div>
</div>

<script>
    document.addEventListener("DOMContentLoaded", function () {
        var url = "/assets/Quentin_CAUDRON.pdf";
        var loadingTask = pdfjsLib.getDocument(url);
        var pdfDoc = null;
        var scale = 1.0; // Default zoom
        var pdfContainer = document.getElementById("pdf-container");

        function renderPages() {
            pdfContainer.innerHTML = ""; // Clear previous renders

            for (let num = 1; num <= pdfDoc.numPages; num++) {
                pdfDoc.getPage(num).then(function (page) {
                    var viewport = page.getViewport({ scale: scale });

                    var canvas = document.createElement("canvas");
                    var context = canvas.getContext("2d");
                    canvas.width = viewport.width;
                    canvas.height = viewport.height;

                    pdfContainer.appendChild(canvas);

                    var renderContext = { canvasContext: context, viewport: viewport };
                    page.render(renderContext);
                });
            }
        }

        loadingTask.promise.then(function (pdf) {
            pdfDoc = pdf;
            renderPages(); // Initial render
        });

        // Zoom Controls
        document.getElementById("zoomIn").addEventListener("click", function () {
            scale += 0.2;
            renderPages();
        });

        document.getElementById("zoomOut").addEventListener("click", function () {
            if (scale > 0.5) {
                scale -= 0.2;
                renderPages();
            }
        });

        document.getElementById("downloadPdf").addEventListener("click", function () {
            window.open(url, "_blank");
        });
    });
</script>
