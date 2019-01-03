# prova2
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- These tags are needed for enabling experimental Chrome APIs via Chrome's Origin-Trial program (Android, Windows): https://github.com/GoogleChrome/OriginTrials/blob/gh-pages/available-trials.md#current-experimental-features -->
    <!-- Origin Trial Token, feature = Generic Sensors, origin = https://github.io, expires = 2018-04-10 -->
    <meta http-equiv="origin-trial" data-feature="Generic Sensors" data-expires="2018-04-10" content="Aokv0ODVMUPIswIBi6DnpAIjhWefEd8gD8GpVgdYgETj0C5+/3kKMzZE/FOrBwHcpBO6LHuVRrIw3yOT8EMmJAYAAABQeyJvcmlnaW4iOiJodHRwczovL2dpdGh1Yi5pbzo0NDMiLCJmZWF0dXJlIjoiR2VuZXJpY1NlbnNvciIsImV4cGlyeSI6MTUyMzMxODQwMH0=">
    <!-- Origin Trial Token, feature = WebVR (For Chrome M62+), origin = https://github.io, expires = 2018-05-07 -->
    <meta http-equiv="origin-trial" data-feature="WebVR (For Chrome M62+)" data-expires="2018-05-07" content="AgINztgDnjFV8da2D9SSzIITBRlHX8mduCR7DXfENxjr9ALduKOxBDdn2n66auQSlljVyhnRWWerxC0BWbE8pAoAAABOeyJvcmlnaW4iOiJodHRwczovL2dpdGh1Yi5pbzo0NDMiLCJmZWF0dXJlIjoiV2ViVlIxLjFNNjIiLCJleHBpcnkiOjE1MjU3MjU4MDh9">
    <title>provawebvr | webvr</title>
    <meta name="description" content="prova1">
    <link rel="icon" href="favicon.ico">
    <link rel="stylesheet" type="text/css" href="styles/webvr.css">
    <script src="lib/telemetry.js"></script>
    <script>
      MozillaResearch.telemetry.start({
        analytics: true,
        errorLogging: true,
        performance: true
      });
      MozillaResearch.telemetry.performance.mark('LoaderParsingStart');
    </script>
    <script src="Build/UnityLoader.js"></script>
    <script>
      /* global UnityLoader, MozillaResearch */
      MozillaResearch.telemetry.performance.measure('LoaderParsing', 'LoaderParsingStart');
      (function () {
        UnityLoader.SystemInfo.mobile = false;  // Workaround to force `UnityLoader` to actually load on mobile.
        MozillaResearch.telemetry.performance.mark('LoadingStart');
        window.gameInstance = UnityLoader.instantiate('gameContainer', 'Build/web vr prova2.json', {
          Module: {
            // `preserveDrawingBuffer` is needed for WebVR content to be mirrored to the `<canvas>`.
            webglContextAttributes: {
              preserveDrawingBuffer: true
            }
          },
          onProgress: unityProgress
        });

        function unityProgress (gameInstance, progress) {
          if (!gameInstance.progress) {
            gameInstance.loader = document.getElementById('loader');
            gameInstance.progress = document.getElementById('progress');
            gameInstance.loading = document.getElementById('loading');
            document.dispatchEvent(new CustomEvent('UnityProgressStart'));
          }
          gameInstance.progress.style.width = (100 * progress) + '%';
          if (progress === 1) {
            document.dispatchEvent(new CustomEvent('UnityLoaded'));
          }
        }
      })();
    </script>
    <link rel="manifest" href="manifest.webmanifest">
  </head>
  <body>
    <div id="loader">
      <div id="loading" class="loading">Loading</div>
      <div id="progress" class="progress"></div>
    </div>

    <div id="game">
      <div id="gameContainer"></div>
    </div>

    <div id="instruction">
      <div id="novr" class="panel center">
        <h3>You&rsquo;ll need a <a href="https://webvr.rocks/">WebVR-enabled browser</a> and VR headset to fully enjoy this experience.</h3>
        <p><img src="mousedrag.png" width="70" alt="Click-and-drag your mouse"></p>
        <p>In the meantime, <strong><em>click and drag</em></strong> to have a look around!</p>
        <p>
          <button class="confirm">Continue</button>
        </p>
      </div>
    </div>

    <button id="entervr" value="Enter VR"></button>

    <div id="performance" data-enabled="false"></div>

    <script src="vendor/gl-matrix-min.js"></script>
    <script src="vendor/webvr-polyfill.min.js"></script>
    <script src="webvr.js"></script>
  </body>

</html>
