# yolov8_colab_image
<b> yolov8을 이용하고 이미지를 바탕하면에 저장하고 yolov8을 사용하였습니다.

필요한 라이브러리 설치
YOLO 모델을 사용하기 위해 ultralytics, opencv-python-headless, matplotlib 라이브러리를 설치합니다.

파일 업로드
Google Colab 환경에 이미지를 업로드할 수 있도록 files.upload()를 사용하여 로컬 시스템에서 파일을 선택하고 업로드합니다.

업로드된 파일 이동
업로드된 이미지를 Colab 환경의 /content/sample_data/ 폴더로 이동시킵니다.

YOLO 모델 불러오기
YOLO('yolov8n.pt')로 사전 학습된 YOLOv8n 모델을 로드합니다.

이미지 경로 정의
업로드한 이미지의 경로를 설정하여 YOLO 모델이 해당 이미지를 처리할 수 있게 합니다.

객체 감지 실행
YOLO 모델을 사용해 이미지에서 객체 감지를 실행하고, 그 결과를 results에 저장합니다.

감지된 결과 저장
감지된 객체의 결과를 새로운 이미지로 저장합니다.

결과 이미지 경로 정의
결과 이미지의 경로를 설정하고, 해당 경로에 저장된 이미지를 표시할 준비를 합니다.

결과 이미지 표시
감지된 객체가 표시된 결과 이미지를 Colab 화면에 출력합니다.



``` bash
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
```


![5](https://github.com/user-attachments/assets/5ee3f5dd-9436-4c8c-bdd8-72f8b56b6886)
