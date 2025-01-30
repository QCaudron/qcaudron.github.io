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
    }

    /* Wrapper for proper layout */
    #pdf-wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 20px;
        width: 100%;
        max-width: 1200px;
    }


    /* Toolbar properly styled */
    #pdf-toolbar {
        width: 120%;
        max-width: 1080px;
        background: #333;
        display: flex;
        justify-content: center;
        gap: 10px;
        padding: 10px;
        color: white;
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
        max-width: 1080px;
        background: white;
        box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
        border-radius: 8px;
        text-align: center;
    }

    canvas {
        display: block;
        margin: 10px auto;
        max-width: 100%;
        height: auto;
    }

    .zoom-icon {
        color: white;
        font-weight: bold;
        font-size: 20px;
    }
</style>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.14.305/pdf.min.js"></script>
<!-- <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/4.10.38/pdf.min.mjs"></script> -->

<!-- Wrapper to ensure it stays inside the content area -->
<div id="pdf-wrapper">
    <div id="pdf-toolbar">
        <button id="downloadPdf"><span class="zoom-icon">⬇ </span> Download resume</button>
        <button id="downloadPdfPub"><span class="zoom-icon">⬇ </span> Download resume with publications</button>
    </div>
    <div id="pdf-container"></div>
</div>

<script>
    document.addEventListener("DOMContentLoaded", function () {
        var url = "/assets/Quentin_CAUDRON.pdf";
        var urlpub = "/assets/Quentin_CAUDRON_pub.pdf";
        var loadingTask = pdfjsLib.getDocument(url);
        var pdfDoc = null;
        var scale = 2.0; // Max zoom
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

        document.getElementById("downloadPdf").addEventListener("click", function () {
            window.open(url, "_blank");
        });
        document.getElementById("downloadPdfPub").addEventListener("click", function () {
            window.open(urlpub, "_blank");
        });
    });
</script>
