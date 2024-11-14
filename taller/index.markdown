---
layout   : page
title    : Las Matemáticas en el Procesamiento Digital de Imágenes
categoria: opencv
date     : 2024-11-13 21:00:00 -0600
# Taller de Visión Computacional
---

Google Colab: <https://colab.research.google.com>{:target="_blank"} 

| Recurso | Archivo | 
| --- | --- |
| Imagen 1 | ![Tablero](tablero.png) |
| Imagen 2 | <https://www.elheraldodetabasco.com.mx/doble-via/los-10-misterios-arqueologicos-y-antropologicos-de-tabasco-7140561.html>{:target="_blank"} |
| Imagen 3 | ![Tablero](partitura.png){: width="300px"} |
| Imagen 4 | Buscar 'hadwritten text' en <https://pixabay.com>{:target="_blank"} |
| Imagen 5 | Buscar 'faces' en <https://depositphotos.com>{:target="_blank"} |
| Video | Buscar 'people walking' en <https://pixabay.com/es/videos/>{:target="_blank"} |

<!-- https://pixabay.com/es/videos/ser%C3%ADa-aptitud-f%C3%ADsica-ejercicio-117545/
https://pixabay.com/es/videos/marioneta-sombra-persona-control-1405/ -->

### YOLO en video

```python
%%time
heat_map_annotator = sv.HeatMapAnnotator()
bbox_annotator = sv.BoxAnnotator()
label_annotator = sv.LabelAnnotator()

# Bucle principal
with sv.VideoSink(target_path=RESULTADO, video_info=info) as sink:
    for frame in sv.get_video_frames_generator(source_path=VIDEO, stride=2):
        resultado = modelo(frame, verbose=False)[0]
        detecciones = sv.Detections.from_ultralytics(resultado)
        frame = heat_map_annotator.annotate(scene=frame.copy(), detections=detecciones)
        frame = bbox_annotator.annotate(scene=frame.copy(), detections=detecciones)
        etiquetas = []
        for class_id,confidence in zip(detecciones.class_id, detecciones.confidence):
            etiquetas.append(f'{modelo.model.names[class_id]} {confidence:.2f}')
        frame = label_annotator.annotate(scene=frame.copy(), detections=detecciones, labels=etiquetas)

        sink.write_frame(frame=frame)
        #plt.imshow(frame)
        #break

sv.VideoInfo.from_video_path(video_path=RESULTADO)
```