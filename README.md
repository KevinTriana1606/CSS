# MOMENTO 2 - MISION DE APROPIACION (TRABAJO INDIVIDUAL)

Catalogo semantico de productos desarrollado en HTML5 y CSS3, con enfasis en
maquetacion semantica, herencia, selectores combinados, jerarquia de
especificidad CSS y anatomia espacial (modelo de caja).

## ESTRUCTURA DEL PROYECTO

index.html   -> Maquetado semantico del catalogo
style.css    -> Hoja de estilos (herencia, selectores combinados, cascada y modelo de caja)
README.md    -> Documentacion tecnica y calculo de especificidad

## MAQUETADO SEMANTICO IMPLEMENTADO

header     -> Encabezado del sitio
nav        -> Barra de navegacion principal
ul, li, a  -> Listas y enlaces de navegacion
main       -> Zona central con los productos
section    -> Agrupa las 4 tarjetas de producto
article    -> Cada tarjeta de producto (titulo h2, descripcion p, precio p
              y enlace de compra a)
aside      -> Barra lateral con menu secundario de categorias
footer     -> Derechos de autor y enlaces a redes sociales

## HERENCIA

En la etiqueta body se declararon:

font-family: sans-serif;
color: #333333;

Los encabezados, parrafos y listas heredan estos valores sin declararlos uno
por uno, lo que demuestra la herencia del navegador.

## SELECTORES COMBINADOS (PINTURA AISLADA POR ZONAS)

Menu principal   -> header nav ul li a   -> 4 pts
Menu lateral     -> aside ul li a        -> 4 pts
Redes sociales   -> footer ul li a       -> 4 pts

Cada zona tiene su propio color de enlace, por lo que modificar el menu
secundario no afecta al menu principal ni al pie de pagina.

## CALCULO DE PUNTOS DE ESPECIFICIDAD

Tipo de selector   Peso      Ejemplo           Puntos
Etiqueta           1 pt      article, a, p     1
Clase              10 pts    .btn-comprar      10
ID                 100 pts   #btn-destacado    100

## Calculo de las reglas del proyecto

header nav ul li a  -> 1 + 1 + 1 + 1  -> 4 pts
aside ul li a       -> 1 + 1 + 1 + 1  -> 4 pts
footer ul li a      -> 1 + 1 + 1 + 1  -> 4 pts
.btn-comprar        -> 10             -> 10 pts

## RETO 2 - CONFLICTO DE AUTORIDAD (CASCADA VS ESPECIFICIDAD)

Al enlace de compra destacado se le asignaron simultaneamente:

## En el HTML

href="#" class="btn-comprar" id="btn-destacado">Comprar
En el CSS, antes de refactorizar:
btn-destacado { color: #000000; }  -> 100 pts, declarada ARRIBA
.btn-comprar   { color: #c62828; }  -> 10 pts, declarada ABAJO

Resultado: el enlace se mostro de color #000000 y no de color #c62828.
Aunque la clase estaba declarada despues (orden de cascada), el ID con
100 pts aplasto a la clase con 10 pts. Conclusion: la especificidad pesa
mas que el orden de aparicion.

Esa version anterior quedo registrada como comentario dentro de style.css
para dejar evidencia del experimento.

## REFACTORIZACION (ESTANDARIZACION DE LA ESPECIFICIDAD)

Se elimino la regla basada en id y el diseno quedo resuelto con un sistema
plano basado exclusivamente en etiquetas y clases:

.btn-comprar { color: #d32f2f; }

No se uso !important en ningun punto del CSS.
La colision visual se resolvio usando solo la clase, sin recurrir a IDs.
El estilo de cada zona se mantiene aislado con selectores combinados.

## ANATOMIA ESPACIAL (ESTRUCTURA SIN FLEXBOX NI GRID)

Para distribuir las cajas principales de la interfaz, se usaron tecnicas
tradicionales de CSS:
 Se aplico box-sizing: border-box; en el selector universal * para que los
  elementos no crezcan de mas al agregar rellenos y bordes.
 El cuerpo de la pagina se dividio en supercajas (con colores suaves).
 El aside ocupa el 25% a la izquierda usando float: left.
 El main ocupa el 75% a la derecha usando float: right.
 El footer usa clear: both para obligarse a si mismo a bajar y ubicarse
  siempre en la parte inferior.
 Los articulos (tarjetas de producto) usan display: inline-block con un
  ancho del 48% para lograr una cuadricula de dos columnas.
 Se aplico padding: 20px y margin: 1% a los articulos para inyectar aire
  interno y separarlos entre si.
 Se aplico una imagen de fondo al header con background-image, ajustando
  su tamano con background-size: cover y su posicion con
  background-position: center.

## HALLAZGOS: EL MODELO DE CAJA

1. Diferencia practica entre Margin y Padding
El padding es el espacio interno de una caja. Separa el contenido (texto,
enlaces, imagenes) del borde de la propia caja y se pinta con el color de
fondo del elemento. El margin es el espacio externo. Separa la caja de sus
elementos vecinos y no se pinta con el fondo del elemento. En resumen, el
padding da aire hacia adentro y el margin empuja hacia afuera.

2. Por que es obligatorio usar box-sizing: border-box
Por defecto el navegador usa content-box. Esto significa que si a un elemento
le declaras width: 100px y le agregas 20px de padding y 1px de borde por
lado, el ancho real en pantalla sera 142px. Esto rompe la maqueta porque los
elementos crecen mas de lo planeado.
Al usar border-box, el padding y el borde se calculan dentro del ancho
declarado. Si pides 100px, esos 100px incluyen el contenido, el padding y el
borde. El elemento respeta el tamano asignado y la estructura se mantiene
estable sin hacer calculos matematicos manuales.

3. Como se ven afectados los elementos hermanos cuando a uno se le aplica un
   margen grande
Al aplicar un margen grande a un hermano, este empuja a los demas. Si a un
article se le pone un margin-bottom grande, el elemento que esta debajo se
vera desplazado hacia abajo. Ademas, en CSS los margenes verticales de dos
elementos hermanos se colapsan. Es decir, no se suman. Si el primer elemento
tiene un margen inferior de 40px y el segundo un margen superior de 15px, el
espacio real entre ellos sera de 40px (se toma el valor mayor).

## VERSIONADO

git add .
git commit -m "feat(ui): implementar modelo de caja y backgrounds"
git push origin feature/modelo-caja

## COMO VISUALIZARLO

1. Clonar el repositorio.
2. Abrir index.html en el navegador o usar Live Server en VS Code.
3. Inspeccionar los elementos con DevTools (pestana Computed o Calculado) haciendo clic sobre un producto para comprobar que el padding de 20px, el margin de 1% y el display: inline-block coinciden exactamente con el codigo programado en css

## Hallazgos: Centralización de Identidad Visual y Espaciado

### 1. Lista completa de variables declaradas

**Colores
 `--color-primario: #1e88e5;`
 `--color-secundario: #6a1b9a;`
 `--color-fondo: #ffffff;`
 `--color-texto: #333333;`
 `--color-texto-titulo: #222222;`
 `--color-texto-medio: #444444;`
 `--color-texto-suave: #666666;`
 `--color-texto-invertido: #ffffff;`
 `--color-acento: #d32f2f;`
 `--color-fondo-header: #e3f2fd;`
 `--color-fondo-aside: #f3e5f5;`
 `--color-fondo-articulo: #fafafa;`
 `--color-fondo-footer: #eceff1;`
 `--color-titulo-aside: #4a148c;`
 `--color-enlace-aside: #6a1b9a;`
 `--color-enlace-aside-hover: #9c27b0;`
 `--color-texto-footer: #546e7a;`
 `--color-borde-articulo: #e0e0e0;`
 `--color-borde-aside: #e1bee7;`
 `--color-borde-footer: #cfd8dc;`

**Tipografía**
 `--fuente-principal: 'Poppins', sans-serif;`

**Espaciado**
 `--espaciado-pequeno: 8px;`
 `--espaciado-medio: 16px;`
 `--espaciado-grande: 24px;`

### 2. Ventaja de reutilizar medidas de margen y relleno

En lugar de inventar un valor distinto en cada selector (10px aquí, 20px allá),
usar tokens garantiza que todas las tarjetas, secciones, header, aside y footer
compartan exactamente la misma proporción de aire. Si mañana el cliente pide más
separación general, basta con editar `--espaciado-grande` en un único punto y toda
la interfaz se actualiza de forma coherente, sin riesgo de dejar espacios desiguales.

### 3. Cómo `:root` previene colisiones visuales al crecer la hoja de estilos

Al centralizar la paleta, la tipografía y la escala de espaciado en `:root`, cualquier
selector nuevo que se agregue en el futuro reutiliza los mismos tokens en vez de
introducir valores arbitrarios. Esto evita que dos secciones "casi iguales" terminen
con tonos o separaciones ligeramente distintas, y convierte a `:root` en la única
fuente de verdad del sistema de diseño: si un color o espaciado debe cambiar, se
cambia una vez y no en decenas de reglas dispersas.
