# Chapter 1. 컴퓨터 그래픽스의 개요

GUI: Graphical User Interface
렌더링: Rendering
텍스처 매핑: Texture Mapping
VRML: Virtual Reality Modeling Language
GPU: Graphics Processing Unit
응용프로그래밍 인터페이스(API): Application Programming Interface
국제표준: de-facto standard
좌표계: Coordinate system
도형: 3D(2D(점 point, 선 line, 다각형 polygon, 원 circle, 곡선 curve), 다면체 polyhedron, 곡면 surface)

벡터 그래픽스: Vector Graphics
 - SVG: Scalable Vector Graphics

래스터 그래픽스: Raster Graphics
 - 비트맵 그래픽스: Bitmap Graphics
 - 픽셀(Pixel): Picture Element
 - 페인팅: Painting

모델링: Modeling
 - 와이어프레임: Wire-frame
 - 다각형 표면: Polygon Surface
 - 솔리드 모델링: Solid Modeling

투영: Projection
렌더링: Rendering
 - 관찰자: Viewer
 - 은면 제거: Hidden Surface Removal
 - 광원: Light Source
 - 셰이딩: Shading
 - 텍스처 매핑: Texture Mapping
 - 광선추적법: Ray Tracing

이미지 처리: Image Processing
가상공간: Cyberspace
애니메이션: Animation
가상현신: Virtual Reality

# Chapter 2. 컴퓨터 그래픽스 시스템

그래픽스 가속기: Graphics Accelerator
프레임 버퍼: Frame Buffer
CRT: Cathode Ray Tube
전자총: Electron Gun
전자빔: Cathode Ray
형광체: Phosphor
해상도: Resolution
스캔라인: scanline
종횡비: Aspect Ratio
제어 그리드: Control Grid
주사: Scan
깜빡힘: Flicker
활성화: Refresh
벡터 모니터: Vector Monitor
래스터 모니터: Raster-Scan Monitor
지그재그: Jaggies
(안티)앨리어싱: (Anti)Aliasing
컬러 모니터: Color Monitor
빔주사 방식: Bean Penetration
섀도우 마스크: Shadow Mask
강도: Intensity
dpi: Dot Per Inch
CMYK: Cyan Magenta Yellow blacK

# Chapter 3. WebGL과 그래픽스 응용 소프트웨어

WebGL 기본 제공 형상 모델
 - 면: Plane
 - 상자: Box
 - 원: Circle
 - 구: Sphere
 - 원뿔: Cone
 - 원통: Cylinder
 - 텍스트: Text
정점: Vertex
선분: Edge
변환(Transformation)
 : Viewing 변환, Modeling 변환, Projection 변환, Viewport 변환
평행 투영: Parallel Projection
원근 투영: Perspective Projection

**3.2.3 3차원 객체의 은면제거 (Hidden Surface Removal)**

깊이 검사: Depth Test
컬링: Culling

**3.2.4 색상 및 셰이딩 (Color and Shading)**

셰이딩(Shading)
 - 기본 셰이딩: Flat Shading
 - Ground Shading
 - 퐁 셰이딩: Phong Shading
블렌딩: Blending

# Chapter 4. 2차원 그래픽스의 기본 요소

속성: Attributes
주사 변환: Scan Conversion

점(Point)
 - 크기: Size
 - 명암: Intensity
 - 색상: Color
 - 모양: Shape

선(Line)
 - 선의 유형: Line Type
 - 선의 굵기: Width
 - 선끝 모양: Line Cap

다중선(Polyline)
 - 선 이음(Line Join): 없음(No Join), 연장이음(Miter Join), 원형이음(Round Join), 경사각이음(Bevel Join)

DDA AL(Digital Differential Analyzer Algorithm)
 - 기울기: Slope
 - 절편: intercept

8방향 대칭: Eight-way symmetry

**4.2 원, 타원 및 기타 곡선**

극좌표계: Polar Coordinate
브레젠헴: Bresenham

**4.3 다각형 채우기**

홀짝 규칙: Even-Odd Rule
접기횟수 규칙: Non-zero Winding Rule
다각형 주사변환: Polygon Scan-Conversion
활성화 엣지 목록(AEL): Active Edge List
방향: dir
응집성: Coherence

**4.6 색상의 표현**

색상보기표(CLUT): Color Look-Up Table

# Chapter 5. 2차원 그래픽스의 변환

**5.1 기본적인 기하변환 (Geometric Transformation)**

 이동: Translation
  - 이동벡터: Translation Vector
  - 더하기 연산: Addition
 신축 확대/축소: Scale
  - 신축배율: Scaling Factor
  - 곱하기 연산: Multiplication
  - 원점: Origin
회전: Roatation
 - 회전각: Rotation Angle

**5.2 동차좌표계를 이용한 변환**

동차좌표계(HCS): Homogeneous Coordinate System
 - 이동변환: Translate Transformation
 - 신축변환: Scale Transformation
 - 회전변환: Rotate Transformation
 - 합성변환: Composite Transformation
참조점: Reference Point

**5.4 래스터 방식에서의 변환**

래스터 연산: RasterOP
 - 고무줄: Rubber Band
비트블릿(bitBlt): Bit Block Transfer
 - 펌웨어: Firmware
 - 비트 연산: Bitwise Operation

**5.5 윈도와 뷰포트**

뷰잉 파이프라인: Viewing Pipeline
줌잉: Zooming
패닝: Panning

**5.6 클리핑 알고리즘 (Clipping Algorithm)**

점 클리핑: Point Clipping
선 클리핑: Line Clipping
 - Cohen-Sutherland Al: 영역비트 (Region Bit), 영역코드 (Region Code)
다각형 클리핑: Polygon Clipping
 - 속이 찬 다각형: Filled Polygon
 - Sutherland-Hodgeman(Polygon Clipping Al)
