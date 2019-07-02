# TensorRT를 이용한 OCR Model Inference 성능 최적화

## 카카오 OCR 모델 구조
* Detection + Recognizer

## Text Detection Model
* Text Detector

## Recognition Model
* Convolu + Self-Attention

## OCR INference 최적화
* 학습된 모델 압축 -> TensorRT 활용

## Optimization with TensorRT

* Precision Calibration
* Keep Accuracy
  * Quantization-awrare trainin
  * Int8: Network Quantization
* Kernel Auto-Tuning
  * Optimizes kernel selection

## Apply TensorRT to TensorFlow Model

* TensorFlow Graph -> UFF Network -> TensorRT Engine -> Inference

## Course to apply

1. TensorFlow Save
  * Trans tensorrt format
2. tfgraph to UFF
  * plugin layer
  * graph surgeon
3. TensorRT Engine
  * Int8: quantization

### Data type check
* output, input float32!!
* cast nono

### Check tensorrt shape
* 가변길이 -> 고정길이 input
* shape 고정

### graph check
* tf.layers.dense / tf.layers.conv1d -> tf.layers.conv2d!!!

## Plugin layer을 이용한 연산 구현 
* UFF Conversion을 통한 미지원 연산 확인
* IPluginV2
* Enqueue-Layer 연산
  * Cudnn/Cublas 라이브러리 활용 (BatchMatmul)

## Graph Surgeon 을 이용한 Plugin 적용
* Forwarding을 통한 그래프 수정
  1. Input forwarding - 노드 제거
  2. Plugin layer 연산으로 변경 (Cast_1)

## TensorRT Engine 생성 및 Inference
* TensorRt Engine 생성
  * UFF 네트워크의 input / Output parsing
* FP16/INT8 Quantization
  * Fp16: 바로 적용 가능
  * Int8: Network calibration 수행
* INt8 Calibration
  * 8-bit integer: -127~127
  * TnsorRT calibration 사용

## TensorTR Inference 성능 분석
* 디텍터 성능
* 인퍼런스 성능

## OCR Inference 성능 요약
* 디텍터 / 레코그나이저
  * 속도/지피유메모리 사용
