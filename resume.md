---
title: Resume
permalink: /resume/
weight: 20
---


<object data="/assets/Quentin_CAUDRON.pdf" width="1000" height="1000" type='application/pdf'></object>

<!-- 
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.14.305/pdf.min.js"></script>

<style>
    body {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        min-height: 100vh;
        background-color: #f4f4f4;
        margin: 0;
    }
    #pdf-viewer {
        width: 80%;
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

<div id="pdf-viewer"></div>

<script>
    var url = "/assets/Quentin_CAUDRON.pdf"; // Replace with your actual PDF file
    var loadingTask = pdfjsLib.getDocument(url);

    loadingTask.promise.then(function(pdf) {
        var viewer = document.getElementById("pdf-viewer");

        for (let pageNum = 1; pageNum <= pdf.numPages; pageNum++) {
            pdf.getPage(pageNum).then(function(page) {
                var scale = 1.5;
                var viewport = page.getViewport({ scale: scale });

                var canvas = document.createElement("canvas");
                var context = canvas.getContext("2d");
                canvas.width = viewport.width;
                canvas.height = viewport.height;

                viewer.appendChild(canvas);

                var renderContext = { canvasContext: context, viewport: viewport };
                page.render(renderContext);
            });
        }
    });
</script> -->
