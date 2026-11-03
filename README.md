Momento 2 - Mision de Apropiacion (Trabajo Individual)

Catalogo semantico de productos desarrollado en HTML5 y CSS3, con enfasis en
maquetacion semantica, herencia, selectores combinados y jerarquia de
especificidad CSS.


ESTRUCTURA DEL PROYECTO

index.html   -> Maquetado semantico del catalogo
style.css    -> Hoja de estilos (herencia, selectores combinados y cascada)
README.md    -> Documentacion y calculo de especificidad


MAQUETADO SEMANTICO IMPLEMENTADO

header     -> Encabezado del sitio
nav        -> Barra de navegacion principal
ul, li, a  -> Listas y enlaces de navegacion
main       -> Zona central con los productos
section    -> Agrupa las 4 tarjetas de producto
article    -> Cada tarjeta de producto (titulo h2, descripcion p, precio p
              y enlace de compra a)
aside      -> Barra lateral con menu secundario de categorias
footer     -> Derechos de autor y enlaces a redes sociales


HERENCIA

En la etiqueta body se declararon:

font-family: sans-serif;
color: #222222;

Los encabezados, parrafos y listas heredan estos valores sin declararlos uno
por uno, lo que demuestra la herencia del navegador.


SELECTORES COMBINADOS (PINTURA AISLADA POR ZONAS)

Menu principal   -> header nav ul li a   -> 4 pts
Menu lateral     -> aside ul li a        -> 4 pts
Redes sociales   -> footer ul li a       -> 4 pts

Cada zona tiene su propio color de enlace, por lo que modificar el menu
secundario no afecta al menu principal ni al pie de pagina.


CALCULO DE PUNTOS DE ESPECIFICIDAD

Tipo de selector   Peso      Ejemplo           Puntos
Etiqueta           1 pt      article, a, p     1
Clase              10 pts    .btn-comprar      10
ID                 100 pts   #btn-destacado    100

Calculo de las reglas del proyecto:

header nav ul li a  -> 1 + 1 + 1 + 1  -> 4 pts
aside ul li a       -> 1 + 1 + 1 + 1  -> 4 pts
footer ul li a      -> 1 + 1 + 1 + 1  -> 4 pts
.btn-comprar        -> 10             -> 10 pts


RETO 2 - CONFLICTO DE AUTORIDAD (CASCADA VS ESPECIFICIDAD)

Al enlace de compra destacado se le asignaron simultaneamente:

En el HTML:
<a href="#" class="btn-comprar" id="btn-destacado">Comprar</a>

En el CSS, antes de refactorizar:
#btn-destacado { color: #000000; }  -> 100 pts, declarada ARRIBA
.btn-comprar   { color: #c62828; }  -> 10 pts, declarada ABAJO

Resultado: el enlace se mostro de color #000000 y no de color #c62828.
Aunque la clase estaba declarada despues (orden de cascada), el ID con
100 pts aplasto a la clase con 10 pts. Conclusion: la especificidad pesa
mas que el orden de aparicion.

Esa version anterior quedo registrada como comentario dentro de style.css
para dejar evidencia del experimento.


REFACTORIZACION (ESTANDARIZACION DE LA ESPECIFICIDAD)

Se elimino la regla basada en id y el diseno quedo resuelto con un sistema
plano basado exclusivamente en etiquetas y clases:

.btn-comprar { color: #c62828; }

No se uso !important en ningun punto del CSS.
La colision visual se resolvio usando solo la clase, sin recurrir a IDs.
El estilo de cada zona se mantiene aislado con selectores combinados.


VERSIONADO

git commit -m "feat(styles): maquetar catalogo semantico y aplicar jerarquia CSS"
git push origin develop


COMO VISUALIZARLO

1. Clonar el repositorio.
2. Abrir index.html en el navegador o usar Live Server en VS Code.
3. Inspeccionar los elementos con DevTools para comprobar la herencia y la
   especificidad aplicada a cada enlace.