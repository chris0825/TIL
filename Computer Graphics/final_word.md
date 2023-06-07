## Chapter 06.
- CUI = Character User Interface
- GUI = Graphical User Interface
- 커서 = Cursor
- 일관성 = Consistency
- 예측성 = Predictability
- 안정성 = Stability
- 피드백 = Feedback
### 6.2.2 물리적(Physical) 입력장치
  - 위치장치 = Locator Device
    - 지시장치 = Pointing/Positioning Device
  - 획 = Stroke
  - 수치장치 = Valuator Device
    - 전위차계 = Potentiometer
  - 선택장치 = Choice Device
    - PFK = Programmable Function Key
  - 문자열장치 = String Device
### 6.3.1 위치지정 기법 = Positioning Technique
  - 고무줄 기법 = Rubber-Band Technique
  - 드래깅 기법 = Dragging Technique
  - 제한 기법 = Constraint Technique
  - 격자 기법 = Grid Technique
  - 스케치 기법 = Sketching Technique
### 6.3.2 지적/선택 기법 = Picking/Selection Technique
  - 시작적 피드백 = Visual Feedback
  - 핸들 기법 = Handle Technique
  - 중력장 기법 = Gravity Field Technique
  - 선택레벨 = Selection Level
  - 그룹핑 = Grouping
### 6.4.1 탐색항해 = Navigation
  - 둘러보기 = Traveling
    - 운전 = Steering
    - 목적지 지정 = Target-based
    - 시점 조작 = Viewpoint Manipulation
  - 길찾기 = Wayfinding
    - 지도 = Map
    - 모형 = Miniature
    - 표지판 = Landmark
### 6.4.2 선택(Selection) 및 조작(Manipulation)을 위한 기법
- 선택/지적 = Selection/Picking
- 조작 = Manipulation
  - 참조 객체 = Reference Object

## Chapter 07.
### 7.1 3차원 그래픽스의 처리과정
- 모델링 = Modeling: 3D Object Representation
  - 다각형 표면 모델링 = Polygon Surface Modeling
  - 곡면 모델링 = Parametric Surface Modeling
  - 솔리드 모델링 = Solid Modeling
  - 스위핑 = Sweeping
  - 프랙탈 = Fractal
  - 입자 시스템 = Particle System
  - 와이어 프레임 = Wireframe
  - 매개변수 = Parameter
  - 곡면 = Curved
- 투영 = Projection
  - WC = World Coordinate
  - 투영선 = Projection line
  - 투영면 = Projection plane
  - 시점 = Viewpoint
  - 평행(직각) 투영 = Parallel Projection
  - 원근 투영 = Perspective Projection
### 7.2.1 이동(Translation)
### 7.2.2 신축(확대/축소: Scale)
### 7.2.3 회전(Rotation)
### 7.3.3 좌표계의 변환
- 역행렬 = inverse matrix
## 7.4 투영(Projection)의 개념과 종류
### 7.4.2 투영의 종류
- 평행 투영 = Parallel Projection
  - 직각 투영 = Orthographic Projection
  - 등축 투영 = Axonometric Projection
    - 삼축 투영 = Isometric Projection
  - 경사 투영 = Oblique Projection
- 원근 투영 = Perspective Projection
  - 시점 = View Point
### 7.5 뷰잉 변환(Viewing Transformation)
### 7.5.2 뷰잉 좌표계(Viewing Coordinate System)
- 뷰평면 기준점(VRP) = View Reference Point
- 뷰평면 법선벡터(VPN) = View Plane Normal Vector
- 뷰업벡터(VUP) = View Up Vector
### 7.6.1 뷰 볼륨(View Volume)
- 프러스텀 뷰볼륨 = Frustum View Volume
### 7.6.2 평행 투영(Parallel Projection)의 변환행렬
- 직각 투영 = Orthographic Projection
- 경사 투영 = Oblique Projection
### 7.6.3 원근 투영(Perspective Projection)의 변환행렬
## Chapter 08.
### 8.1 객체 모델링의 개요
- 다각형 메쉬 = Polygon Mesh
- 베지어 곡면 = Bezier Curved
- 스위핑 = Sweeping
- 조립적 입체기하학(CSG) = Constructive Solid Geometry
- 블러비 객체 = Blobby Object
### 8.2 다각형면(Polygon Surface) 모델링
### 8.2.1 다각형 메쉬(Polygon Mesh) 표현
- 삼각 메쉬법 = Triangular Mesh
- 사각 메쉬법 = Quadrilateral Mesh
- 다각형 간략화 = Polygon Simplification
### 8.2.2 기하적 데이터 표(Geometric Data Table)
### 8.2.3 평면 방정식(Plane Equation)
- 법선벡터 = Normal Vector
- 안쪽 = Inside
- 바깥쪽 = Outside
### 8.3.1 2차 곡선과 곡면(Quadrics and Quadric Surface)
- 원뿔 곡선 = Conic Section
- 원 = Circle
- 구 = Sphere
- 타원 = Ellipse
- 타원체 = Ellipsoid
- 포물선 = Parabola
- 포물면 = Paraboloid
- 토러스 = Torus
### 8.3.2 수퍼 2차 곡선과 곡면(Superquadrics)
- 수퍼타원 = Superellipse
- 수퍼타원체 = Superellipsoid
### 8.4 스플라인(Spline) 곡선
- 다항식 = Polynomial
- 보간 곡선 = Interpolation
- 근사 곡선 = Approximation
### 8.4.3 3차 스플라인(Cubic Spline) 곡선
### 8.5.1 베지어 곡선(Bezier Curve)
- 베지어 다항식 = Bezier Polynomial
- 배합함수 = Blending Function
- 영향 = Weight
- 볼록 다각형 = Convex Hull
### 8.5.2 베지어 곡면(Bezier Surface)
## Chapter 09.
- 은면 = Unvisible Hidden
- 보이는 면 = Visible Surface
### 9.1 은면제거(Hidden Surface Removal)
- 뒷면 제거 = Backface Culling
- 현실감 = Realism
- 은선제거 = Hidden Line Removal
- 객체공간법 = Object Space Method
- 깊이정렬 알고리즘 = Depth Sorting = Painter's Algorithm
- 이미지공간법 = Image Space Method
- z-버퍼 알고리즘 = z-Buffer = Depth Buffer Algorithm
### 9.1.2 은면제거의 처리 개념
- 정렬 = Sorting
- 일관성 = Coherence
- 공간적 일관성 = Spatial Coherence
- 시간적 일관성 = Temporal Coherence
- 포함영역 = Extent
### 9.3.2 다면체 뒷면의 제거(Back-Face Removal)
- 색상값 = Intensity
## 9.5 레이케스팅(Ray-Casting) 기법
- 광선 = Ray
- 만나는 점 = Hit Point
- 광선추적법 = Ray Tracing
