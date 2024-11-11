# yolov8_colab_image
<b> yolov8을 이용하고 이미지를 바탕하면에 저장하고 yolov8을 사용하였습니다
~~~ vash
# 필요한 라이브러리 설치
%pip install ultralytics opencv-python-headless matplotlib

# 파일 업로드를 위한 라이브러리 import
from google.colab import files

# 이미지 파일 업로드
uploaded = files.upload()

# 업로드된 파일의 이름을 가져옴
filename = next(iter(uploaded))

# 이미지 파일을 Colab 환경으로 이동
!mkdir -p /content/sample_data
!mv {filename} /content/sample_data/{filename}

# YOLO 라이브러리와 이미지 출력 함수 import
from ultralytics import YOLO
from IPython.display import Image, display

# YOLOv8n 모델 불러오기 (사전 학습된 모델)
model = YOLO('yolov8n.pt')

# 이미지 경로 정의
image_path = '/content/sample_data/' + filename

# 모델을 사용하여 이미지에서 객체 감지 실행
results = model(image_path)

# 첫 번째 결과 가져오기 (감지된 객체가 있는 첫 번째 이미지)
first_result = results[0]

# 감지된 결과 저장
first_result.save()

# 결과 이미지 경로 정의
saved_image_path = '/content/runs/detect/exp/' + filename

# 결과 이미지 표시
display(Image(saved_image_path))
~~~
