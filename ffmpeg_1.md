# Section 1

- https://ibm-learning.udemy.com/course/ffmpeg-the-complete-guide/learn/lecture/26884126#overview

## What is FFmpeg?

- Fast Forward Moving Picture Experts Group
- For transcoding/streaming
- C

### FFmpeg libraries

- libavcodec: codecs
- libavformat: formats
- libavfilter: filters to modify streams
- etc

## Setting up FFmpeg

- no official build

### Build variants

- master branch x release branch
	- 6개월쯤 주기로 메이저 업데이트 有
- static x dynamic


# Section 2

## ffprobe

- `ffprobe video.mp4`
	- 온라인 영상으로도 가능 (다운 필요 없음)
	- 첫 줄은 ffprobe가 무슨 config으로 빌드되었는지 보여줌
- `ffprobe -v error video.mp4`
	- 에러가 있을 시에만 프린트 함
- `ffprobe -v error video.mp4 -show_format`
- `ffprobe -v error video.mp4 -show_format -show_streams -print_format json`
	- 각 stream 의 정보, json 으로
- `ffprobe -v error video.mp4 -show_streams -select_streams v`
	- 영상 관련 정보만 보여줌
- `ffprobe -v error video.mp4 -select_streams v -show_entries stream=codec_name`
	- 코덱 이름만 보여줌
	- `-print_format default=noprint_wrappers=1`
	- `-print_format default=noprint_wrappers=1:nokey=1`

## ffplay

- 영상/오디오/사진/링크 다 가능
- `ffplay -v error video.mp4 -x 600 -y 600`
	- 플레이어 창 크기
- `-noborder`
- `-y 600`: 그러면 자동으로 계산해서 검은 부분 없음
- `-top 0 -left 0`: 화면에서 재생 위치
- `-fs`: fullscreen
- `-an`: 소리 없이
- `-vn`: 영상 없이
- `-showmode waves`: 오디오 웨이브만 보여줌
- `-loop 0`: 루프 & 횟수 (0은 평생)

- 숏컷
	- 소리 업다운 0 / 9
	- F: fullscreen
	- S: frame step

# Section 3

## Fundamentals of Media

- pixel: RGB or YUV && alpha (transparency)
- audio frequency => how many samples in seconds
- video compression: spatial & temporal redundancy

## Codecs and Containers

- Co(der)dec(oder)
	- encode: compression / decode: play or editing
	- H.264, H.265, VP9 (압축 적음) / PCM (압축 적음), AAC, MP3
- Container
	- package/wrapper for the media essence
	- how the media is organized inside a file
	- header / index / track 1 / track 2
	- MP4, MXF, QT/MOV, MKV / WAV, M4A
- 컨테이너 안에 비디오 코덱과 오디오 코덱이 들어있는 거

## Transcoding

- 