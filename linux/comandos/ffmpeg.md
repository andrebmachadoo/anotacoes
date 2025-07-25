# ffmpeg
---

> FFmpeg é uma ferramenta de linha de comando gratuita e de código aberto para transcodificar arquivos multimídia. Incluindo o conjunto de bibliotecas compartilhadas de áudio e vídeo, como libavcodec, libavformat e libavutil. Com o FFmpeg, você pode converter formatos de vídeo e áudio, definir taxas de amostragem e redimencionar vídeos.

```sh
#Para exibir os encoders e decoders do FFmpeg

$ ffmpeg -encoders
$ ffmpeg -decoders

#Converter um arquivo de vídeo .mp4 para .webm
$ ffmpeg -i input-file.mp4 output-file.webm

#Converter um arquivo de áudio .mp3 para .ogg
$ ffmpeg -i input-file.mp3 output-file.ogg

#Convertendo um arquivo de áudio .mp4 para .webm usando o codec de vídeo libvpx e codec de áudio libvorbis
$ ffmpeg -i input-file.mp4 -c:v libvpx -c:a libvorbis output-file.webm

#Convertendo um arquivo de áudio .mp3 para .ogg codificado com o codec libopus
$ ffmpeg -i input-file.mp4 -c:a libopus output-file.ogg


$ ffmpeg -i video2.avi -b 300k -r 15 -ar 22050 -ab 32 -f flv -s 320x240 video2.flv
```

|Parametros | Descrição|
|--|--|
| -b bitrate|Set the video bitrate in bit/s (default = 200 kb/s).|
| -r frame rate | To force the frame rate of the input file (valid for raw formats only) to 1 fps and the frame rate of the output file to 24 fps.|
| -ar freq | Set the audio sampling frequency (default = 44100 Hz).|
|-ab bitrate | Set the audio bitrate in bit/s (default = 64k). |
|`-f fmt' | Force format.| 
|`-s size' | Set frame size. The format is `wxh' (ffserver default = 160x128, ffmpeg default = same as source). The following abbreviations are recognized:
||`sqcif'|
||128x96|
||`qcif'|
||176x144|
||`cif'|
||352x288|
||`4cif'|
||704x576|
||`qqvga'|
||160x120|
||`qvga'|
||320x240|
||`vga'|
||640x480|
||`svga'|
||800x600|
||`xga'|
||1024x768|
||`uxga'|
||1600x1200|
||`qxga'|
||2048x1536|
||`sxga'|
||1280x1024|
||`qsxga'|
||2560x2048|
||`hsxga'|
||5120x4096|
||`wvga'|
||852x480|
||`wxga'|
||1366x768|
||`wsxga'|
||1600x1024|
||`wuxga'|
||1920x1200|
||`woxga'|
||2560x1600|
||`wqsxga'|
||3200x2048|
||`wquxga'|
||3840x2400|
||`whsxga'|
||6400x4096|
||`whuxga'|
||7680x4800|
||`cga'|
||320x200|
||`ega'|
||640x350|
||`hd480'|
||852x480|
||`hd720'|
||1280x720|
||`hd1080'|
||1920x1080|

|||
|-|-|
|Mais... |http://ffmpeg.arrozcru.org/builds/|