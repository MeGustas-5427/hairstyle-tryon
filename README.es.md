# Hairstyle Try-on · Prueba virtual de peinados

[English](README.md) | [简体中文](README.zh-CN.md) | Español | [Français](README.fr.md) | [Português](README.pt.md) | [Русский](README.ru.md) | [한국어](README.ko.md) | [日本語](README.ja.md)

Una skill de Codex para recibir recomendaciones realistas de peinados y probarlos virtualmente a partir de un selfi.

Proporciona un selfi y, si quieres, una imagen del peinado que te gustaría tener. Codex recomienda 4–6 propuestas completas según las características de tu cabello y tu rutina diaria. Después de que elijas tus favoritas, imagegen integrado genera una foto de prueba por propuesta, junto con una página comparativa y una ficha en lenguaje sencillo para compartir con tu peluquero o peluquera.

## Ejemplos

Resultados de 4 pruebas con fotos de bancos de imágenes: 12 imágenes generadas por IA. Son simulaciones, no fotos de cortes reales antes y después ni recomendaciones de las personas retratadas. W02 incluye ampliación del lienzo hacia abajo; el cuello, la ropa y el fondo añadidos son inferidos por IA.

[Ver los 12 resultados, comparaciones y créditos](examples/README.md)

| Original | Prueba con IA |
| --- | --- |
| **P02**<br><a href="examples/p02/original.webp"><img src="examples/p02/original.webp" alt="P02 Original" width="320"></a> | **H02 · Flequillo rizado**<br><a href="examples/p02/h02.webp"><img src="examples/p02/h02.webp" alt="P02 Prueba con IA: Flequillo rizado" width="320"></a> |
| **W02**<br><a href="examples/w02/original.webp"><img src="examples/w02/original.webp" alt="W02 Original" width="320"></a> | **H01 · Bob francés castaño cálido**<br><a href="examples/w02/h01.webp"><img src="examples/w02/h01.webp" alt="W02 Prueba con IA: Bob francés castaño cálido" width="320"></a> |
| **W03**<br><a href="examples/w03/original.webp"><img src="examples/w03/original.webp" alt="W03 Original" width="320"></a> | **H04 · Bob liso con gafas**<br><a href="examples/w03/h04.webp"><img src="examples/w03/h04.webp" alt="W03 Prueba con IA: Bob liso con gafas" width="320"></a> |

## Cómo funciona

1. Proporciona un selfi frontal y nítido. Las fotos de perfil, de la parte posterior de la cabeza y del peinado deseado son opcionales.
2. Elige las opciones que describan tu cabello, si aceptarías una permanente o un tinte, cuánto tiempo dedicarías al peinado y qué quieres evitar. También puedes responder «No lo sé» o escribir tu propia respuesta.
3. Consulta propuestas con imágenes de referencia, motivos de la recomendación, requisitos para conseguir el resultado y enlaces a las fuentes.
4. Selecciona 1–3 propuestas por defecto; se genera una foto por cada una. Puedes pedir más de forma explícita.
5. Revisa las fotos individuales y la comparación en paralelo; después, solicita ajustes indicando el identificador de la propuesta.

Los peinados se organizan por longitud y características, para personas de cualquier género. El peinado de referencia se adapta a las condiciones de tu cabello. Cada generación utiliza tu selfi original como referencia de tu apariencia.

## Requisitos

Este repositorio contiene instrucciones de una skill, no un modelo de imágenes, un servicio de API ni la implementación de un plugin. Requiere un entorno de Codex que permita usar skills locales, ver imágenes y utilizar imagegen integrado.

| Herramienta | Uso | Si no está disponible |
| --- | --- | --- |
| imagegen integrado en Codex | Generar y editar fotos de prueba | Conservar las propuestas y explicar la limitación; nunca cambiar automáticamente a una API de pago |
| Exa (opcional) | Opción preferente para buscar y consultar fuentes sobre peinados | Recurrir a una búsqueda web convencional |
| TypeSafe (opcional) | Filtrar y ordenar las descripciones de las propuestas | Codex se encarga de la selección |
| Interactive Form Save (opcional) | Recoger preferencias, selecciones múltiples y leer las respuestas enviadas | Usar opciones numeradas y respuestas de texto libre |

El flujo con imagegen integrado no requiere configurar `OPENAI_API_KEY`. La disponibilidad, las cuotas y las condiciones de las herramientas externas dependen de sus respectivos servicios; este repositorio no incluye acceso a ellos.

## Instalación

Clona o extrae este repositorio en una carpeta llamada `hairstyle-tryon`, dentro del directorio de skills configurado en tu Codex:

```text
tu-directorio-de-skills/
└── hairstyle-tryon/
    ├── SKILL.md
    ├── README.md
    ├── README.zh-CN.md
    ├── README.es.md
    ├── README.fr.md
    ├── README.pt.md
    ├── README.ru.md
    ├── README.ko.md
    ├── README.ja.md
    ├── examples/
    └── LICENSE
```

Si tienes configurado `CODEX_HOME`, puedes usar su subdirectorio `skills`. Antes de instalar, comprueba si ya existe una carpeta con ese nombre y conserva cualquier cambio local. Evita colocar los archivos dentro de dos carpetas `hairstyle-tryon` anidadas.

## Uso

Invoca la skill en Codex y adjunta tu foto. Por ejemplo:

```text
Usa $hairstyle-tryon para ayudarme a encontrar un peinado para ir a trabajar.
Quiero mantener mi color actual, sin permanente, y dedicar unos 5 minutos al día a peinarme.
Voy a subir un selfi frontal. Déjame elegir varias propuestas antes de generar las fotos de prueba.
```

Si tienes una imagen del peinado deseado, adjúntala también e indica qué rasgos te interesa conservar. Después puedes pedir cambios como: «Acorta un poco el flequillo de H02 y deja todo lo demás igual».

## Resultados

Por defecto, los resultados se guardan en `output/hairstyle-tryon/<identificador-unico-de-ejecucion>/` dentro del espacio de trabajo de la tarea. Puedes indicar otro directorio.

- Una foto de prueba por propuesta, con un nombre que incluye su identificador y versión.
- `comparison.html`: una página comparativa en paralelo que referencia la foto original y las generadas.
- `notes.md`: fuentes, instrucciones de generación, resultados de la revisión y una ficha para cada peinado.

La ficha del peinado es una nota sencilla que puedes mostrar en la peluquería: qué rasgos quieres conservar, qué cambios aceptas, cómo te peinas a diario y qué aspectos deben evaluarse en persona. No es una receta de corte ni una garantía del resultado.

## Validación y uso de imágenes

La versión de la skill es `v0.1.0`. Cuatro pruebas con fotos de bancos de imágenes produjeron 12 resultados con imagegen integrado el 2026-09-28 y el 2026-10-12; las comprobaciones visuales y de archivos se documentan en la [galería](examples/README.md). El proceso con un selfi del propio usuario y los resultados de cortes reales siguen sin validarse. La conservación de la apariencia depende de las instrucciones y de la revisión visual, sin garantía de coincidencia píxel a píxel.

El repositorio contiene la skill, documentación y demostraciones seleccionadas en `examples/`, sujetas a sus [créditos y condiciones de uso de imágenes](examples/CREDITS.md). No contiene selfis de usuarios ni formularios privados. Las fotos de cada ejecución se utilizan para esa solicitud. Antes de publicar, revisa los archivos preparados para el commit para evitar incluir fotos privadas, resultados ajenos o credenciales. `.gitignore` sigue excluyendo las carpetas de salida y de entrada local habituales.

## Contacto

Grupo de QQ: `1094787834`.

## Licencia

Las instrucciones de la skill y la documentación se distribuyen bajo la [licencia MIT](LICENSE). El texto estándar está disponible en la [Open Source Initiative](https://opensource.org/license/mit). Esta licencia no concede derechos adicionales sobre fotos de usuarios, imágenes de referencia de Internet ni servicios externos.
