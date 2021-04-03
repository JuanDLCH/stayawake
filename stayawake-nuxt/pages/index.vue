<template>
  <body>
    <link
      rel="stylesheet"
      href="https://unpkg.com/flickity@2.2.2/dist/flickity.css"
    />

    <script src="https://unpkg.com/flickity@2.2.2/dist/flickity.pkgd.min.js"></script>
    <!-- Encabezado -->
    <header>
      <!-- Menu de navegacion -->
      <div class="navegacion">
        <nav>
          <nuxt-link to="/"
            ><img src="@/static/img/stayawakelogo.svg" alt="logo" class="logo"
          /></nuxt-link>
          <ul>
            <li><nuxt-link to="/">Inicio</nuxt-link></li>
            <li><nuxt-link to="/#origen">Origen</nuxt-link></li>
            <li><nuxt-link to="/#objetivo">Objetivo</nuxt-link></li>
            <li><nuxt-link to="/#nosotros">Nosotros</nuxt-link></li>
            <li>
              <nuxt-link to="/#contactanos">Contactanos</nuxt-link>
            </li>
          </ul>
        </nav>

        <div class="principal">
          <div class="textocentrado">
            <h1>StayAwake</h1>
            <p>
              Protegemos tu vida y la de los demás actores viales en la
              carretera, creamos consciencia en la via y salvamos la vida de
              muchos conductoresy pasajeros de ser victimas de accidentes por
              microsueños.
            </p>
            <p>¡Mantente despierto!</p>
            <p>Tu familia te espera.</p>
          </div>
        </div>

        <div class="login">
          <div class="loginitems">
            <h1>Inicia Sesion</h1>

            <div class="textbox">
              <label for="txtemail">Correo Electronico:</label>
              <input type="email" name="correo" id="txtemail" />
            </div>

            <div class="textbox">
              <label for="txtpass">Contraseña:</label>
              <input type="password" name="pass" id="txtpass" />
            </div>

            <div class="button">
              <input type="submit" value="Ingresar" />
            </div>

            <a href="">¿Olvidaste tu contraseña?</a>

            <p>¿No tienes cuenta? <a href="">Registrate</a></p>
          </div>
        </div>
      </div>
    </header>

    <!-- Cuerpo -->
    <main>
      <section id="origen">
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
                    Buscamos aumentar la seguridad en la carretera incentivando
                    a los conductores a no dormirse al volante y a no aburrirse
                    al conducir, de modo que puedan estar más atentos en la vía
                    y no sean un peligro para ellos mismos y para los demás.
                  </p>
                </div>
              </div>
              <div class="gallery-cell">
                <div class="textocentrado">
                  <p class="intro">
                    Si un conductor tiene un microsueño mientras se desplaza a
                    80 kilómetros por hora puede llegar a recorrer 45 metros sin
                    ningún tipo de atención o reacción, generando graves riesgos
                    para la integridad del conductor y los pasajeros. Una de las
                    causas de accidente de tránsito en carretera identificada
                    por las empresas transportadoras es el agotamiento en los
                    conductores por las largas jornadas de trabajo.
                  </p>
                </div>
              </div>
              <div class="gallery-cell">
                <div class="textocentrado">
                  <p class="datos">
                    Según datos reunidos en Colombia,
                    <cite
                      >durante 2019, más de 184 personas han terminado con
                      lesiones, como consecuencia de los microsueños, ya sea
                      directamente al ser conductores de vehículos o cuando
                      viajan como pasajeros.
                    </cite>
                    <br />
                    <br />
                    De acuerdo con las autoridades de tránsito, las horas en las
                    que el sueño tiene mayor incidencia en los conductores, se
                    ubican entre las dos y las cuatro de la tarde, y en las
                    noches entre las dos y las cinco de la madrugada,
                    <br />
                    incluso si se ha dormido previamente al viaje, situación que
                    demanda mayor precaución.
                  </p>
                </div>
              </div>
              <div class="gallery-cell">
                <div class="textocentrado">
                  <p class="caso">
                    Jorge es un conductor de una compañía que transporta
                    mercancía y su trabajo es viajar entre Medellín y Cartagena,
                    Jorge lleva muchos años en este oficio y se conoce la
                    carretera como nadie. Un día Jorge cumplió con su jornada de
                    trabajo sin problemas, desafortunadamente no descansó lo
                    suficiente ese día ya que debía realizar algunas diligencias
                    personales,
                  </p>
                </div>
              </div>
              <div class="gallery-cell">
                <div class="textocentrado">
                  <p class="caso">
                    Esa noche inició nuevamente su jornada de operación, pero
                    todo fue distinto, Jorge se sentía agotado y por momentos no
                    reaccionaba como de costumbre, la carretera que tanto
                    conocía le estaba jugando una mala pasada. Dicen que cuando
                    las cosas pueden salir mal se ponen peores y así fue para
                    Jorge ese día, a su agotamiento se sumaron baja visibilidad
                    por neblina y en el momento menos pensado un automóvil que
                    frena en carretera hacen que Jorge pierda el control y
                    choque contra una casa al borde de la carretera, en
                    condiciones normales Jorge habría reaccionado sin problemas,
                    pero este día sus reflejos no lo acompañaron. Fueron las
                    últimas horas de conducción de Jorge, ese día murió en
                    carretera y ocasionó la tragedia más grande para una familia
                    que se encontraba descansando en casa.
                  </p>
                </div>
              </div>
              <div class="gallery-cell">
                <div class="textocentrado">
                  <p class="caso">
                    En condiciones normales Jorge habría reaccionado sin
                    problemas, pero este día sus reflejos no lo acompañaron.
                    Fueron las últimas horas de conducción de Jorge, ese día
                    murió en carretera y ocasionó la tragedia más grande para
                    una familia que se encontraba descansando en casa.
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section id="objetivo">
        <div class="fondo">
          <dl>
            <dt>
              <h1>Objetivo:</h1>
            </dt>
            <dd>
              <p>
                Como estudiantes, buscamos brindar una solucion para esta
                problematica y reducir la tasa de mortalidad por accidentes en
                la carretera gracias a los microsueños, no culpamos a los
                conductores, conducir se torna monótono cuandos se hace por
                varias horas, y aún más en la noche que es cuando más suelen
                circular los camiones, queremos atacar este punto, reduciendo la
                monotonía al manejar y brindandole a los conductores un pequeño
                asistente en la palma de su mano que les ayude a permanecer
                despiertos de una forma didáctica sin necesidad de distraerlos
                de su labor
              </p>
            </dd>
          </dl>
        </div>
      </section>

      <section id="nosotros">
        <dl>
          <dt>
            <h1>Sobre nosotros:</h1>
          </dt>
          <dd>
            <p>
              Somos un grupo de 5 estudiantes de 5to semestre de la Universidad
              de Medellin de la carrera de Ingeniería de Sistemas interesados en
              superarnos cada día e innovar para el servicio y la calidad de
              vida de las personas.
            </p>
          </dd>
        </dl>

        <h2>¿Quiénes somos?</h2>
        <div class="container">
          <ul>
            <li>
              <div class="item">
                <!--Imagen-->
                Juan Diego Londoño Chavarría
              </div>
            </li>
            <li>
              <div class="item">
                <!--Imagen-->
                Mario Alejandro Saldarriaga Alvarez
              </div>
            </li>
            <li>
              <div class="item">
                <!--Imagen-->
                Jhon Mario Aviles Ruiz
              </div>
            </li>
            <li>
              <div class="item">
                <!--Imagen-->
                Jader Daniel Atehortúa Zapata
              </div>
            </li>
            <li>
              <div class="item">
                <!--Imagen-->
                Pablo González Velasquez
              </div>
            </li>
          </ul>
        </div>
      </section>
    </main>

    <!-- Footer -->
    <footer>
      <section id="contactanos">
        <h1>Contactanos</h1>
        <div>
          <ul>
            <li><a href="mailto:stayawakeproject@yopmail.com">Correo</a></li>
            <li>Direccion</li>
            <li>Telefono</li>
          </ul>
        </div>
        <div>
          <h3>Mapa</h3>
          <!--Mapa-->
        </div>
      </section>
    </footer>
  </body>
</template>

<script>
export default {}
</script>

<style>
/* General */

body {
  margin: 0;
  padding: 0;
  background: black;
}

h1 {
  color: white;
}

a {
  color: white;
}

p {
  color: white;
}

label {
  color: white;
}

h2 {
  color: white;
}

/* Barra de navegacion */
header {
  height: 100vh;
  width: 100%;
  position: relative;
}

.logo {
  height: 90%;
  width: 10%;
  margin: 5px;
}

nav {
  align-items: center;
  content: '';
  position: fixed;
  height: 10vh;
  bottom: 0;
  right: 0;
  left: 0;
  top: 0;
  background: rgba(0, 0, 0, 0.65);
  z-index: 4;
}
nav ul {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  justify-content: center;
  align-items: center;
  list-style-type: none;
  margin-top: 0;
  height: 5vh;
}

nav li {
  margin: 7px;
}

nav a {
  color: white;
  text-decoration: none;
  font-size: 20px;
}

nav a:hover {
  font-size: 23px;
  color: rgb(184, 184, 184);
}

/* Imagen de inicio */

.navegacion {
  height: 100vh;
  width: 100%;
  background: url('@/static/img/camionmontanas.jpg');
  background-size: 100% 100%;
  position: absolute;
  display: flex;
}

/* Texto inicio */

.principal {
  z-index: 1;
  width: 70%;
  height: 100vh;
  float: left;
  text-align: center;
  position: relative;
  background: rgba(0, 0, 0, 0.452);
}

.textocentrado {
  color: white;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  width: 60%;
}

.textocentrado h1 {
  margin-top: 0;
  font-size: 50px;
  margin-bottom: 0;
}

.textocentrado p {
  font-size: 20px;
  margin-top: 10px;
  color: rgb(255, 255, 255);
}

/* Login */

.login {
  z-index: 3;
  width: 30%;
  height: 100vh;
  float: right;
  text-align: center;
  position: relative;
  background: rgba(0, 43, 68, 0.849);
  box-shadow: -21px -1px 3px rgba(0, 0, 0, 0.356);
}

.loginitems {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.textbox {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.textbox input {
  width: 250px;
  margin-bottom: 20px;
}

.button input {
  margin-bottom: 20px;
  width: 40%;
}

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

/*cell number 
  .gallery-cell:before {
    display: block;
    text-align: center;
    content: counter(gallery-cell);
    line-height: 200px;
    font-size: 80px;
    color: white; 
  } */

/* Objetivo */

#objetivo {
  height: 50vh;
  width: 100%;
  background: url(/stayawake/src/static/img/ruta.jpg);
}
</style>