<template>
  <section id="origen">
    <link
      rel="stylesheet"
      href="https://unpkg.com/flickity@2.2.2/dist/flickity.css"
    />

    <script src="https://unpkg.com/flickity@2.2.2/dist/flickity.pkgd.min.js"></script>
    <div class="fondo">
      <div class="tituloIzquierda">
        <h1>Origen</h1>
      </div>
      <div class="carrusel">
        <!-- Flickity HTML init -->
        <div
          class="gallery js-flickity"
          data-flickity-options='{ "wrapAround": true }'
        >
          <div class="gallery-cell">
            <div class="textocentrado">
              <p class="origen">
                Surgimos como equipo de trabajo con un enfoque común:
                <strong
                  >"Proteger la vida de aquellos que más queremos."</strong
                >
                <br />
                Buscamos aumentar la seguridad en la carretera incentivando a
                los conductores a no dormirse al volante y a no aburrirse al
                conducir, de modo que puedan estar más atentos en la vía y no
                sean un peligro para ellos mismos y para los demás.
              </p>
            </div>
          </div>
          <div class="gallery-cell">
            <div class="textocentrado">
              <p class="intro">
                Si un conductor tiene un microsueño mientras se desplaza a 80
                kilómetros por hora puede llegar a recorrer 45 metros sin ningún
                tipo de atención o reacción, generando graves riesgos para la
                integridad del conductor y los pasajeros. Una de las causas de
                accidente de tránsito en carretera identificada por las empresas
                transportadoras es el agotamiento en los conductores por las
                largas jornadas de trabajo.
              </p>
            </div>
          </div>
          <div class="gallery-cell">
            <div class="textocentrado">
              <p class="datos">
                Según datos reunidos en Colombia,
                <cite
                  >durante 2019, más de 184 personas han terminado con lesiones,
                  como consecuencia de los microsueños, ya sea directamente al
                  ser conductores de vehículos o cuando viajan como pasajeros.
                </cite>
                <br />
                <br />
                De acuerdo con las autoridades de tránsito, las horas en las que
                el sueño tiene mayor incidencia en los conductores, se ubican
                entre las dos y las cuatro de la tarde, y en las noches entre
                las dos y las cinco de la madrugada,
                <br />
                incluso si se ha dormido previamente al viaje, situación que
                demanda mayor precaución.
              </p>
            </div>
          </div>
          <div class="gallery-cell">
            <div class="textocentrado">
              <p class="caso">
                Jorge es un conductor de una compañía que transporta mercancía y
                su trabajo es viajar entre Medellín y Cartagena, Jorge lleva
                muchos años en este oficio y se conoce la carretera como nadie.
                Un día Jorge cumplió con su jornada de trabajo sin problemas,
                desafortunadamente no descansó lo suficiente ese día ya que
                debía realizar algunas diligencias personales,
              </p>
            </div>
          </div>
          <div class="gallery-cell">
            <div class="textocentrado">
              <p class="caso">
                Esa noche inició nuevamente su jornada de operación, pero todo
                fue distinto, Jorge se sentía agotado y por momentos no
                reaccionaba como de costumbre, la carretera que tanto conocía le
                estaba jugando una mala pasada. Dicen que cuando las cosas
                pueden salir mal se ponen peores y así fue para Jorge ese día, a
                su agotamiento se sumaron baja visibilidad por neblina y en el
                momento menos pensado un automóvil que frena en carretera hacen
                que Jorge pierda el control y choque contra una casa al borde de
                la carretera, en condiciones normales Jorge habría reaccionado
                sin problemas, pero este día sus reflejos no lo acompañaron.
                Fueron las últimas horas de conducción de Jorge, ese día murió
                en carretera y ocasionó la tragedia más grande para una familia
                que se encontraba descansando en casa.
              </p>
            </div>
          </div>
          <div class="gallery-cell">
            <div class="textocentrado">
              <p class="caso">
                En condiciones normales Jorge habría reaccionado sin problemas,
                pero este día sus reflejos no lo acompañaron. Fueron las últimas
                horas de conducción de Jorge, ese día murió en carretera y
                ocasionó la tragedia más grande para una familia que se
                encontraba descansando en casa.
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

#origen {
  width: 100%;
  height: 100vh;
  background: url('@/static/img/manejando.jpg');
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

.carrusel {
  float: right;
  align-items: center;
  width: 60%;
  height: 100vh;
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

.gallery-cell .caso {
  font-size: 19px;
  width: 100%;
  margin: 0;
}
</style>