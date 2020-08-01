# Test
<!-- <!DOCTYPE html>
<html>
  <head>
    <meta charset='utf-8'>
    <meta http-equiv="X-UA-Compatible" content="chrome=1">

    <link rel="stylesheet" type="text/css" href="stylesheets/stylesheet.css" media="screen">
    <link rel="stylesheet" type="text/css" href="stylesheets/github-dark.css" media="screen">
    <link rel="stylesheet" type="text/css" href="stylesheets/print.css" media="print">

    <title>AnimatedLEDStrip</title>
  </head>

  <body>

    <header>
      <div class="container">
        <h1>AnimatedLEDStrip</h1>
        <h2></h2>

        <section id="downloads">
          <a href="https://github.com/AnimatedLEDStrip" class="btn btn-github"><span class="icon"></span>View on GitHub</a>
        </section>
      </div>
    </header>

    <div class="container">
      <section id="main_content">
        <h1>
<a id="animatedledstrip" class="anchor" href="#animatedledstrip" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>AnimatedLEDStrip</h1>
<h4>The AnimatedLEDStrip set of libraries are meant to make the process of running animations on a LED strip much easier.</h4>
<p>This library also supports running concurrent animations on a LED strip. Multiple animations can be run simultaneously, even over the same part of the strip. See the <a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStrip/wiki">wiki</a> for more information.</p>
<h2>
<a id="structure" class="anchor" href="#structure" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Structure</h2>
<p>The libraries are designed so you have multiple options for how you integrate AnimatedLEDStrip into your project.</p>
<ul>
<li>If you want to have a solution that works out of the box with minimal effort, then you can install the <a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStrip#raspberry-pi-server">server-pi</a> on a Raspberry Pi and use one of the client examples to control it</li>
<li>If you want to make your program into a client, you can import the <a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStrip/blob/master/README.md#client">AnimatedLEDStripClient</a> library.
Examples of this include the <a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStrip#android-client">Android app</a> and the <a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStrip#raspberry-pi-touchscreen-client">Raspberry Pi Touchscreen Client</a>.
Multiple languages are supported, see the library for details.</li>
<li>If you want to control the strip directly from a Kotlin/Java program, you can import the device library for your device
<ul>
<li>If your device isn't supported, you can <a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStripServer/wiki">create a new device library</a>
</li>
</ul>
</li>
</ul>
<h3>
<a id="main-libraries" class="anchor" href="#main-libraries" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Main Libraries</h3>
<p>The main set of libraries includes:</p>
<h4>
<a id="core" class="anchor" href="#core" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a><a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStrip">Core</a>
</h4>
<p>Contains all the animations and generic structure for communicating with LED strips.</p>
<h4>
<a id="server" class="anchor" href="#server" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a><a href="https://github.com/AnimatedLEDStrip/server">Server</a>
</h4>
<p>A library for running a server that runs animations on a LED strip.
The server communicates with clients to start and end animations.
Also contains a command line interface that can be used to monitor and partially control the server.
To create an executable server, this library is combined with a device library and a short main method (see the <a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStrip#raspberry-pi-server">Raspberry Pi Server</a> for an example).</p>
<h4>
<a id="client" class="anchor" href="#client" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a><a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStripClient">Client</a>
</h4>
<p>A library for communicating with a server by sending JSON over socket connections.
See library for a list of supported languages.</p>
<h3>
<a id="device-libraries" class="anchor" href="#device-libraries" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Device Libraries</h3>
<p>Each device that can run LEDs has its own device library.
Currently the only device supported is the Raspberry Pi, but this can be <a href="https://github.com/AnimatedLEDStrip/server/wiki">expanded to more devices</a> in the future:</p>
<ul>
<li>
<a href="https://github.com/AnimatedLEDStrip/device-pi">Raspberry Pi</a> - A device library for running
LEDs on a Raspberry Pi 3B, 3B+ or 4B</li>
</ul>
<h3>
<a id="examples" class="anchor" href="#examples" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Examples</h3>
<h4>
<a id="raspberry-pi-server" class="anchor" href="#raspberry-pi-server" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a><a href="https://github.com/AnimatedLEDStrip/server-pi">Raspberry Pi Server</a>
</h4>
<p>This repository contains an example implementation of a server for a Raspberry Pi.
This can be used as-is with no modification, or can be used as a template for creating servers on Raspberry Pis or other devices.
The repository includes support for installation using <a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStripPiServerExample#install"><code>ansible-pull</code></a>, further simplifying the install process.</p>
<h4>
<a id="raspberry-pi-touchscreen-client" class="anchor" href="#raspberry-pi-touchscreen-client" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a><a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStripGUI">Raspberry Pi Touchscreen Client</a>
</h4>
<p>This repository contains an example of a GUI that uses the AnimatedLEDStripClient library to communicate with an AnimatedLEDStripServer.
Built with <a href="https://tornadofx.io/">TornadoFX</a>, it is designed to run on a Raspberry Pi with the official 7" touchscreen, though it can be run on any device with Java 8 and JavaFX installed.</p>
<h4>
<a id="android-client" class="anchor" href="#android-client" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a><a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStripAndroidControl">Android Client</a>
</h4>
<p>An Android app that uses the AnimatedLEDStripClient library to communicate with an AnimatedLEDStripServer.</p>
<h3>
<a id="other" class="anchor" href="#other" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a>Other</h3>
<h4>
<a id="arduino-library" class="anchor" href="#arduino-library" aria-hidden="true"><span aria-hidden="true" class="octicon octicon-link"></span></a><a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStripCppArduino">Arduino Library</a>
</h4>
<p>Also included in the set of libraries is one written in C++ for Arduinos.
This is the library that started AnimatedLEDStrip.
See our <a href="https://github.com/AnimatedLEDStrip/AnimatedLEDStrip/wiki#history">history</a> for more details.</p>
      </section>
    </div>

    
  </body>
</html>
 -->
