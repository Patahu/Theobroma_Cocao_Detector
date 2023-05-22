Send message if you want the full code

### Testing
1.
![image](https://github.com/Patahu/TheobromaCacaoDetector/assets/55921419/10c66803-d09d-455c-9e69-6b64d024865e)

2.

![image](https://github.com/Patahu/TheobromaCacaoDetector/assets/55921419/b7ad93b4-fcf6-4cbf-8f4b-2df04bf7052b)

### Results

1. Confusion matrix

![confusion_matrix](https://github.com/Patahu/TheobromaCacaoDetector/assets/55921419/21f5d063-5c3b-431f-a975-f42a81b5d09e)
2. Precision Confidence Curve

![P_curve](https://github.com/Patahu/TheobromaCacaoDetector/assets/55921419/a97e94e0-78da-4f13-bef4-02325b560fab)

3. Others

![results](https://github.com/Patahu/TheobromaCacaoDetector/assets/55921419/519d1273-863e-483b-9b76-441fc6c3cce1)

Train
![train_batch1](https://github.com/Patahu/TheobromaCacaoDetector/assets/55921419/4a366b01-13c9-4fa0-988e-df61079f2859)

Val
![val_batch1_labels](https://github.com/Patahu/TheobromaCacaoDetector/assets/55921419/a0fb7d81-897a-4686-98b9-9ae27954c510)

# flutter_pytorch

- flutter plugin to help run pytorch lite models classification for example yolov5 doesn't give support for yolov7
- ios support (can be added following this https://github.com/pytorch/ios-demo-app) PR will be appreciated  

## Getting Started

## Usage
## preparing the model 
- object detection (yolov5)
```python
!python export.py --weights "the weights of your model" --include torchscript --img 640 --optimize
```
example 
```python
!python export.py --weights yolov5s.pt --include torchscript --img 640 --optimize
```
### Installation
To use this plugin, add `pytorch_lite` as a [dependency in your pubspec.yaml file](https://flutter.dev/docs/development/packages-and-plugins/using-packages).
Create a `assets` folder with your pytorch model and labels if needed. Modify `pubspec.yaml` accordingly.

```yaml
assets:
 - assets/models/model_objectDetection.torchscript
 - assets/labels_objectDetection.txt
```

Run `flutter pub get`

#### For release
* Go to android/app/build.gradle
* Add those next lines in the release config
```
shrinkResources false
minifyEnabled false
```
example 
```
    buildTypes {
        release {
            shrinkResources false
            minifyEnabled false
            // TODO: Add your own signing config for the release build.
            // Signing with the debug keys for now, so `flutter run --release` works.
            signingConfig signingConfigs.debug
        }
    }
```

### Import the library

```dart
import 'package:flutter_pytorch/flutter_pytorch.dart';
```

### Load model

Either classification model:
```dart
ObjectDetection model:
```dart
ModelObjectDetection objectModel = await FlutterPytorch.loadObjectDetectionModel(
          "assets/models/yolov5s.torchscript", 80, 640, 640,
          labelPath: "assets/labels/labels_objectDetection_Coco.txt");
```
### Get object detection prediction for an image
```dart
 List<ResultObjectDetection?> objDetect = await _objectModel.getImagePrediction(await File(image.path).readAsBytes(),
        minimumScore: 0.1, IOUThershold: 0.3);
```

### Get render boxes with image
```dart
objectModel.renderBoxesOnImage(_image!, objDetect)
```


#References 
- Code used the same strucute as the package https://pub.dev/packages/pytorch_mobile
- While using the updated code from https://github.com/pytorch/android-demo-app

Get render boxes with image




