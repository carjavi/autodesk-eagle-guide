<p align="center"><img src="https://raw.githubusercontent.com/carjavi/autodesk-eagle-guide/master/img/autodesk-eagle.png" height="100" alt=" " /></p>
<br>
<h1 align="center">Autodesk Eagle Guide</h1> 
<h4 align="right">Jun 23</h4>

<img src="https://img.shields.io/badge/OS-Windows%2011-blue">

<br>


> :warning: **Warning:** Todo el material aquí expuesto es para la versión 6 de Eagle que estoy probando en la última versión.

<h1 align="center">Autodesk Eagle 6</h1> 
<p align="center"><img src="https://raw.githubusercontent.com/carjavi/autodesk-eagle-guide/master/img/eagle6.jpeg" height="200" alt=" " /></p>

## Donde buscar librerías para Eagle?
1.	En la página de Eagle: https://cadsoft.io/resources/libraries/?query=8452
2.	En la página de www.sparkfun.com ofrecen el componente, datasheet y a veces librería.

## Comandos
* help ripup / ayuda del comando Ripup
* ripup ; / desenruta todo
* ripup @; / desenruta los polígonos

## NOTAS Generales
* para poder mover un componente debes activar la capa de origen
* podemos bloquear y desbloquear un componente desde sus propiedades
* en propiedades se puede agrupar o no el nombre del componente al componente (smashed)

## Como copiar (Dispositivo, símbolo, paquete) entre librerías
Sabiendo estos datos de lo que queremos copiar
* library: pinhead_v2
* device: PINHD-1X1.dev
* package: 1X101/OCT.pac
* symbol: PINHD1.sym
* 
### Desde la librería nueva que estamos usando
      Comando: copy PINHD-1X1.dev@pinhead_v2
### Modificación
En la sección para configurar el Paquete
* cambiar la escala (Grid) a mm
* Mover el paquete muy cerca de la referencia/ origen de coordenadas
* figura del componente en la capa: 21 tPlace
* nombre del componente en la capa: 25 tNames
* alor del componente en la capa: 27 tValue

## Como extraer un componente (Dispositivo, símbolo, paquete) de un proyecto a una librería
1.	Menú principal botón ULP “exp-lbrs.ulp” o “exp-project-lbr.ulp”
2.	Opción “Merge to one Library, original library names as prefix for symbol, package…”
3.	Se creara una libreria .LBR con el mismo nombre del proyecto
Nota: revisar “exp-palette.ulp” / “exp2image.ulp”

## Actualizar librería al agregar un archivo en la carpeta LBR
1.	Basta con ir al panel de control de Eagle
2.	Expandir y contraer en la raíz “librería”
3.	Después buscamos la carpeta que acabamos de agregar y la activamos dándole un click  punto gris
4.	Listo

## Copiar de un esquemático a otro 
En un esquemático agrupamos y le damos copiar, en el otro le damos al botón PASTE que tiene un punto amarillo con otro punto negro

## Como generar el Stancil para cortar en una hoja de acetato en laser
### Como generar el archivo GTP
1.	Abrimos el PCB y en el botón de capas solo dejamos activa la capa CREAM  31 (top) o capa 32(bottom)
2.	En el menú botón 3CAM Proccessor
3.	Section: stecil
4.	Capas (31 tCream) y (20 dimesion)
5.	Output: GERBER_RS274X
6.	Nombre: Nombre_stencil.gtp
7.	Proccess job
Listo.

> :memo: **Note:** Gerber es un formato de archivo que contiene la información necesaria para la fabricación de la placa de circuito impreso o PCB. Se pueden crear con distintos programas de diseño electrónico como PCB Wizard, Eagle, Protel, KiCad o Altium Designer. El estándar más común hoy en día es el RS-274X

## Para tener un archivo para cortar en la Laser
1.	Abrimos el programa GERBV (gerber viewer) y cargamos el archivo que generamos, el gtp
2.	Exportamos a PDF, nota colocarle el .PDF
3.	Abrimos Vcarve e importamos el PDF, configuramos un tamaño adecuado del espacio de trabajo
4.	Desde Vcarve Seleccionamos todos los Vectores y exportamos a DXF
NOTA: no sirve el PDF que genera el eagles, el pdf al vectorizarlo cambia. Autocad no importa un PDF para llevarlo a un DXF.

# Importar una imagen al PCB Board y al  Shematic 
1.	Determinamos las medidas reales a la PCB y en el esquemático. Ejemplo para el esquemático dentro de la caja del FRAME 20x20 mm. En el PCB las medidas en mm.
2.	El logo debe ser una imagen bastante grande superior a los 2000 pixel y tratar de que sea ancho igual al largo.
3.	En Photoshop verificar que tengan colores sólidos y no degradados. Pintar los degradados. En Image/abjusments/ black & White para pasar a blanco y negro. Guardar a BMP (aun no es monocromático).
4.	Abrir con Paint y guardar como  Mapa de Bit Monocromatico.BMP
5.	Si el logo lo vamos a pegar en la capa bottom hay que guardar el logo invertido
6.	Abrimos una librería o creamos una de logos
7.	Creamos un símbolo nuevo con el nombre del logo

## EAGLE Symbol
1.	Creamos el symbolo
2.	En el Menú botón ULP  “import_bmp.ulp”
3.	 tomamos la imagen para capa TOP 
4.	Seleccionar que va a seleccionar el color negro
5.	 Seleccionamos Unit “MM” 
6.	Tomamos la medida real X del tamaño que queremos en el esquemático y la dividimos entre el valor x  que sale en “file data” y el valor lo ponemos en el factor de scala (con 3 cifras significativas). Ejemplo: para el FRAME 20/(el valor en pixel del file data) // PCB la media en mm.
7.	Lo dejamos en la capa 200
8.	Borramos la ruta del archivo que sale al final
9.	salvamos

## EAGLE Paquete
1.	Creamos el paquete con el nombre del logo e indicamos en que capa va
2.	En el Menú botón ULP  “import_bmp.ulp”
3.	 tomamos la imagen para capa TOP  o BOTTOM (importante)
4.	Seleccionar que va a seleccionar el color negro
5.	 Seleccionamos Unit “MM” 
6.	Tomamos la medida real X del tamaño que queremos en el esquemático y la dividimos entre el valor x  que sale en “file data”. En PCB la medida en mm entre file data, el valor lo ponemos en el factor de scala (con 3 cifras significativas). 
7.	En “choose stgar layer” es la capa donde deseamos poner la imagen predefinido 21 TOP y 22 BOTTOM
8.	Borramos la ruta del archivo que sale al final
9.	salvamos

## EAGLE DISPOSITIVO
1.	Creamos el dispositivo y especificamos si el logo es capa TOP o BOTTOM
2.	Cargar el Simbolo 
3.	Cargar paquete
4.	Salvar

## PARA FINALIZAR
1.	En el esquemático agregamos el logo como si fuese un componente
2.	Podemos moverlo como si fuese un componente
3.	Para borrarlo lo agrupamos todo y lo borramos como un grupo
4.	Si queremos modificarlo vamos a la librería y cargamos la imagen con las nuevas dimensiones, en Library/ugdate all actualizamos los cambios en la librería

## Importar un Vector (dxf) para las dimensiones de la PCB
Desde el menú principal de eagle ULP y buscar “import_dxf_polygons_v4.ulp” usar las siguientes características:
– Layer: “Dimension”
– Type: WIRE
– Pen width: 0.0,,,,,,,,,,,,,,, 0.001
NOTA: los archivos DXF no pueden estar muy lejos del origen de coordenadas del programa en donde fue creado sino dará error al importar.
1.	Seleccionamos el objeto mover, y con DYN activado #0,0 enter
2.	Teclear UCS enter y enter

## Medir impedancia, longitud de las pistas 
1.	Botón ULP
2.	Script “length-freq-ri.ulp”

# EN EL SCHEMATIC

NOTA: En el Schematic usar el GRID en esta escala para no tener problema en las conexiones

GRID SIZE: 0.1” = 2.54 mm

GRID ALT: 0.01” = 0.254 mm

En el Schematic intentar no mover estos valores}

> :memo: **Note:* Para mover un componente al GRID (SNAP) selecciono el componente y CTRL +  DOBLE CLICK 

# EN EL PCB:

Medidas más pequeñas
Vías (unión de tierras)……. Drill = 0.3302 mm / 13 mil
                                             
Wires………………………Width = 0.1524 mm / 6 mil
                                       Width = 0.2032 mm / 8 mil

Texto……………………..…Size = 24

> :memo: **Note:**
 OJO Los Componentes SMD deben Buscarse en encapsulado (case) en Pulgadas 0805, 0402, 0603 si  se busca en milímetros cambia el encapsulado.


### Como cambiar el tamaño a los nombres de los componentes 
1.	Ocultamos las capas que no nos sirven
2.	Seleccionamos todos los componentes
3.	En CHANGE / Size seleccionamos el tamaño
4.	Botón derecho Change Group
El grosor en Ratio

### Como poder mover los nombres libremente independiente del componente

Notas:
* Para mover un componente al GRID (SNAP) selecciono el componente y CTRL +  DOBLE CLICK 
* La capa que hace huecos de la tierra de masa está en la capa  tKeepout y bKeepout
* La capa que hace separaciones de la tierra de masa de los pines de los componentes está en la capa  tRestrict y bRestrict
* La capa que tiene la información de los huecos es Drills
* La capa que tiene perforaciones en la tarjeta sin contacto es Holes
* En la capa tDoc está el dibujo de componente
* Es bueno activar los números de los pines en Opciones/set/misc/display pad names

**Observaciones PCB**
* Las tierras deben estar bien tanto en la cara de arriba como abajo con muchas, muchas vías (huecos con continuidad entre placa arriba y abajo). No basta solo líneas gruesas
* Evitar las T en las conexiones
* No poner los componentes tan cerca entre si…las pistas deben pasar entre ellos
* Solo ángulos en las pistas mayores a 90 grados, no ángulos, da ruido

## Duplicar una PCB en el eagles 7
Seleccionamos con la herramientas y abrimos un documento nuevo y con el botón pegar(circulo amarillo y circulo negro) pegamos y duplicamos la PCB.

# PCB en 3D
Para crear renders 3D con este programa necesitamos 3 programas:
* Google SketchUp
* eagleUp
* ImageMagick ( la version 7 no es la ideal) solo la versión 6

1. Copiar de eagleUp4.5\ eagleUp_export.ulp a C:\EAGLE-7.6.0\ulp
2. Copiamos  de eagleUp4.5\ eagleUp_import.rbz a C:\Program Files\SketchUp\SketchUp 2016\ShippedExtensions ( se intala en Ventanas/ preferencias/ extenciones/ import…)
3. copiamos la carpeta models de eagleUp4.5\  a  C:\EAGLE-7.6.0\ulp
4. correr eagleUp_export.ulp en eagle

Llenar la ventana:

<p align="center"><img src="https://raw.githubusercontent.com/carjavi/autodesk-eagle-guide/master/img/pcb-software.png" height="250" alt=" " /></p>

C:\EAGLE-7.6.0\models<br>
C:\Program Files\ImageMagick-6.8.6-Q16\convert.exe<br>
C:\Program Files\ImageMagick-6.8.6-Q16\composite.exe<br>
eagleUp/<br>

ó

ESTA ES MEJOR::::::::
C:\Program Files\ImageMagick-6.7.9-Q8\convert.exe<br>
C:\Program Files\ImageMagick-6.7.9-Q8\ composite.exe<br>

Desde la ventana de PCB goto UPL button y EagleUp_export.ulp (enter)

llenar segunda ventana:

<p align="center"><img src="https://raw.githubusercontent.com/carjavi/autodesk-eagle-guide/master/img/pcb-software2.png" height="300" alt=" " /></p>

Grosor de la tarjeta 1.6<br>
Elegimos color<br>

5.  desde sketchup “Plantilla simple en metros “ Import eagleUp v4.4  y el archive debe estar en el mimo directorio del Proyecto eagle en la carpeta “eagleUP” nombre.eup
6. desde sketchup “Plantilla simple en metros “ ventana/Extensiones/

# Generar lista de componentes
1.	En el esquemático de Eagle  el botón ULP
2.	Scrip “bom.ulp”
3.	En List Type/ Values
4.	En Output format /CSV ( valores separados por coma)
5.	Save y luego Close
6.	Abrirmos con Excel 
7.	Seleccionamos toda la columna A
8.	En pestaña DATOS/elegimos  delimitarlo por punto y coma /next
9.	Separador = punto y coma / next
10.	Formatod de texto = general  / netx
11.	Salvar en Excel.

# Generación de GERBER

Las siguientes son las capas necesarias para poder fabricar de PCB: <br>
Top layer: pcbname.GTL<br>
Bottom layer: pcbname.GBL<br>
Solder Stop Mask top: pcbname.GTS //(Máscara  Antisoldante)<br>
Solder Stop Mask Bottom: pcbname.GBS //(Máscara  Antisoldante)<br>
Silk Top: pcbname.GTO<br>
Silk Bottom: pcbname.GBO<br>
Board Outline: pcbname.GML/GKO<br>
NC Drill: pcbname.TXT  (define el diámetro de las perforaciones)<br>
STENCIL:  *.GTP (top)
                  *.GBP (Bottom)
      


> :memo: **Note:**  El borde de la tarjeta debe estar en un archivo GML o GKO. El archivo de Gerber debe estar
en el formato RS-274X.
 
### Especificaciones:
Color de la Máscaras antisoldantes (color rojo,Azul,Verde  etc.)<br>
Espesor del PCB:<br>
Acabado: Sin Plomo o con plomo <br>
Cantidad de cobre: 1oz ó 2oz<br>


### Otros Formatos Gerber
*. GBL - Gerber capa inferior <br>
*. GTL - Gerber capa superior <br>
*. APG - Gerber parte inferior de soldadura resistir <br>
*. Gts - Gerber superior soldadura resistir <br>
*. GM1 - Gerber mecánica 1 <br>
*. Xln - Excellon taladro archivo <br>
*. Cmp - Top-capa de cobre (componente de lado) <br>
*. Sol - Bajo la capa de cobre (lado de soldadura) <br>
*. STC - Top-capa soldermask (parada máscara) <br>
*. STS - soldermask capa de abajo (sbop máscara) <br>
*. DRD - Excellon taladro archivo <br>
top.gbr - Gerber pistas cara componentes <br>
bot.gbr - Gerber pistas cara soldaduras <br>
masktop.gbr - Gerber componentes de la máscara <br>
maskbot.gbr - Gerber máscara de cara soldaduras <br>
mechanical.gbr - Gerber de control o el tamaño <br>
drill.ncd - Perforación ncdrill<br>
*.cmp (Copper, component side)<br>
*.drd (Drill file)<br>
*.dri (Drill Station Info File) – Usually not needed<br>
*.gpi (Photoplotter Info File) – Usually not needed<br>
*.plc (Silk screen, component side)<br>
*.pls (Silk screen, solder side)<br>
*.sol (Copper, solder side)<br>
*.stc (Solder stop mask, component side)<br>
*.sts (Solder stop mask, solder side)<br>



<br>

---
Copyright &copy; 2022 [carjavi](https://github.com/carjavi). <br>
```www.instintodigital.net``` <br>
carjavi@hotmail.com <br>
<p align="center">
    <a href="https://instintodigital.net/" target="_blank"><img src="https://raw.githubusercontent.com/carjavi/autodesk-eagle-guide/master/img/developer.png" height="100" alt="www.instintodigital.net"></a>
</p>