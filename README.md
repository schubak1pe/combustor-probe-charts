# Probe Charts

Mod de telemetria para **Combustor** (Engine Simulator). Pinta, cuando lo pides,
las graficas de la sonda del motor y resume todo lo que has puesto en el motor.

## Que hace

- **Graficas en vivo** de todos los canales que publica la sonda: empuje, presion
  y temperatura de camara, caudal, Mach de salida, velocidades caracteristicas,
  coeficiente de empuje, impulso especifico, eficiencia, rugosidad, potencias...
- Muestreo a **10 Hz**. En vivo se ve una ventana movil de **60 s**; una
  grabacion conserva todo el tiempo grabado (hasta 12 min) y puedes activar o
  desactivar cada canal.
- **Grabar / Parar**: pulsa **Grabar** para empezar una captura limpia; el panel
  muestra `REC` y el tiempo. Al pulsar **Parar** se congela la captura y se
  genera la grafica de barras de ese registro.
- **Modo barras de 5 s** (por defecto): cada barra resume 5 s del registro y su
  altura es el mayor salto del tramo (rango max-min y cambio de media respecto
  al tramo anterior). Un pico o un cambio brusco se ve como una barra mas alta.
  El boton **Lineas / Barras 5s** alterna ambos modos.
- **Sonda**: estado del ajuste, geometria medida y *todos* los parametros que has
  puesto en la sonda (direccion, origen, camara, garganta, salida, plano,
  suavizado y gravedad de referencia).
- **Montaje**: resumen de lo que hay en el motor: inyectores (gas, caudal,
  temperatura, presion maxima), valvulas, pistones, filtros, turbinas, rejillas
  unidireccionales, encendedores y ajustes de la simulacion.
- **Exportar CSV**: guarda las series y un TXT con la foto completa de la sonda y
  del montaje.
- **Exportar PNG**: guarda una imagen del panel tal como lo ves, con las barras
  o las lineas y sus valores. Si la captura recortada falla, guarda una captura
  de pantalla completa como respaldo.

## Como se abre

- Tecla **F8**.
- Chip **PROBE / F8** en la esquina inferior derecha cuando el panel esta cerrado.
- Boton **Graficas de la sonda (F8)** en el menu de pausa.

El panel se arrastra desde la cabecera. La rueda del raton desplaza las listas.
Mientras el raton esta encima, el juego no recibe los clics.

## Instalacion

1. Cierra Combustor.
2. Copia `CombustorProbeCharts.dll` a
   `...\steamapps\common\EngineSimulator\Mods\`.
3. Abre el juego. En `MelonLoader\Latest.log` debe aparecer
   `Probe Charts ready`.

Requiere MelonLoader 0.7.x y los Il2CppAssemblies generados por el juego.

## CSV

Se guarda en:

```
<Juego>\UserData\ProbeCharts\probe_AAAAMMDD_HHMMSS.csv
<Juego>\UserData\ProbeCharts\probe_AAAAMMDD_HHMMSS_meta.txt
```

El CSV usa `;` como separador y cultura invariante (punto decimal). El TXT
incluye la configuracion de la sonda, las medidas y el montaje.

El PNG se guarda en la misma carpeta:

```
<Juego>\UserData\ProbeCharts\probe_AAAAMMDD_HHMMSS.png
```

## Compilar

```
dotnet build -c Release -p:GameDir="C:\Program Files (x86)\Steam\steamapps\common\EngineSimulator"
```

Opcional, para el autotest (arranca un sandbox y un motor de prueba):

```
dotnet build -c Release -p:ProbeChartsSelfTest=true ...
```

## Notas

- Las unidades y el formato de cada canal salen de la propia sonda; los valores
  de la pestana Sonda se muestran en unidades de simulacion.
- El historial de la sonda del juego es de 24 s; este mod mantiene su propia
  ventana de 60 s para las graficas y la exportacion.
- La eficiencia y la rugosidad se muestran en porcentaje, igual que en el HUD.
