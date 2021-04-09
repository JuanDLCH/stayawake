<template>
  <section id="objetivo">
    <link
      rel="stylesheet"
      href="https://unpkg.com/flickity@2.2.2/dist/flickity.css"
    />

    <script src="https://unpkg.com/flickity@2.2.2/dist/flickity.pkgd.min.js"></script>
    <div class="fondo">
      <div class="carrusel2">
        <!-- Flickity HTML init -->
        <div
          class="gallery js-flickity"
          data-flickity-options='{ "wrapAround": true }'
        >
          <div class="gallery-cell">
            <div class="textocentrado">
              <p class="casos">
                Recuerda, cuidarte en la via es también cuidar a los demás
              </p>
            </div>
          </div>
          <div class="gallery-cell">
            <div class="textocentrado">
              <p class="casos">
                Duerme como mínimo 8 horas antes de conducir cualquier vehiculo
              </p>
            </div>
          </div>
          <div class="gallery-cell">
            <div class="textocentrado">
              <p class="casos">
                Mantente bien hidratado durante tu jornada de conducción
              </p>
            </div>
          </div>
          <div class="gallery-cell">
            <div class="textocentrado">
              <p class="casos">
               Mantén tu vista al frente y no sueltes las manos del volante
              </p>
            </div>
          </div>
          <div class="gallery-cell">
            <div class="textocentrado">
              <p class="casos">
                Evita al máximo el uso del celular, en ningun momento te pediremos que lo uses mientras conduces para usar nuestra
              </p>
            </div>
          </div>
          <div class="gallery-cell">
            <div class="textocentrado">
              <p class="casos">
                Detente en un lugar seguro cada cierto tiempo para estirarte, activar tus músculos y oxigenarte.
                Mantente despierto, cuida a los tuyos y a los demás.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style>
/* Origen */

#objetivo {
  width: 100%;
  height: 100vh;
  background: url('@/static/img/autopista.jpg');
  background-size: 100% 100%;
  padding: 0;
}

.fondo {
  display: flex;
  height: 100vh;
  width: 100%;
  background: rgba(0, 0, 0, 0.555);
}

.tituloIzquierda {
  border-start-start-radius: 100%;
  align-items: center;
  text-align: center;
  float: left;
  height: 100%;
  width: 40%;
  background: rgba(10, 23, 216, 0.384);
  box-shadow: 21px -1px 3px rgba(0, 0, 0, 0.356);
}

.tituloIzquierda h1 {
  font-size: 50px;
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: white;
}

.carrusel2 {
  align-items: center;
  width: 60%;
  height: 100vh;
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

* {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

.gallery {
  /*background: rgb(0, 0, 0);*/
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  height: 600px;
  width: 80%;
}

.gallery-cell {
  align-items: center;
  text-align: center;
  width: 100%;
  height: 600px;
  margin-right: 10px;
  margin-left: 10px;
  background: rgba(0, 0, 0, 0.452);
  counter-increment: gallery-cell;
}

.gallery-cell .origen {
  font-size: 27px;
  width: 100%;
  margin: 0;
}

.gallery-cell .intro {
  font-size: 25px;
  width: 100%;
  margin: 0;
}

.gallery-cell .datos {
  font-size: 22px;
  width: 100%;
  margin: 0;
}

.gallery-cell .casos {
  font-size: 30px;
  width: 100%;
  margin: 0;
}
</style>