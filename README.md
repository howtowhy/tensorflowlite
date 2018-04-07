Readme for Tensorflow Lite Components 
==================================
All right reserved @ Jaewook Kang 2018


## About
This repository provides a set of python scripts for easy Tensorflow lite conversion from Tensorflow models.   

## Dependencies
- Tensorflow >= 1.7 (Git clone required)
- Bazel == 0.11.1
- Python2 <= 2.7.12
- Python3 <= 3.6.0

### OS Dependencies
- Validated at OSX 10.11.6
- Validated at Ubuntu 16.04 LTS
- Windows 10 is not validated.


## Installation 
1) Git clone from the [Tensorflow Repository](https://github.com/tensorflow/tensorflow)
```bash
$ git clone https://github.com/tensorflow/tensorflow
```

2) [Install Bazel Building Tool](https://docs.bazel.build/versions/master/install.html)
- First note that you require to install JAVA JDK8 or later

- [For macOS, use homebrew command](https://docs.bazel.build/versions/master/install-os-x.html)
```bash
# for installation
$ brew install bazel 
# for upgrade
$ brew upgrade bazel
```

- [For Ubuntu, use apt-get commnand](https://docs.bazel.build/versions/master/install-ubuntu.html)
```bash
# for installation
$ echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list
$ curl https://bazel.build/bazel-release.pub.gpg | sudo apt-key add -
$ sudo apt-get update && sudo apt-get install bazel
# for upgrade
$ sudo apt-get upgrade bazel
```

3) Git clone this repository 
```bash
$ git clone https://github.com/jwkanggist/tensorflowlite
```

## Components
```bash
tensorflowlite/ -- convertor/       (python modules of tflite convertor )
                |- data/            (Storage for data set)
                |- pb_and_ckpt/     (Storage for pb and ckpt files)
                |- tf-cnn-model/    (git submoduled from https://github.com/jwkanggist/tf-cnn-model)
                |- tf_logs/         (for Tensorboard use)
                |
                |- run_lenet5_save_pb_convertor.py
                |- run_frozen_pb_convertor.py
                |- run_tflite_convertor.py
```

#### Tensorflow to Tensorflow Lite Model Conversion
We now support three-step model coversion from Tensorflow.
```bash
1) graphdef and checkpoint exporting --> 2) frozen graph conversion --> 3) tflite conversion
```
where we  wrap some details of shell commands for the tflite conversion, providing a set of python scripts. 

All scripts are python, so you can run those with `python` command:
```bash
$ python <script_name>
```

- `run_lenet5_save_pb_convertor.py` : 
    - To export graphdef (.pb) and checkpoint (.ckpt) files from Tensorflow model. 
    - where we generate a Lenet5 model, provided by [the author's repo](https://github.com/jwkanggist/tf-cnn-model), as an example.
- `run_frozen_pb_convertor.py`      : 
    - To generate frozen graph  (.pb) by combining graphdef  (.pb) and checkpoint (.ckpt)
    - Where we use (.pb) and (.ckpt) of Lenet5 model generated by `run_lenet5_save_pb_convertor.py`
- `run_tflite_convertor.py`         : 
    - To convert  frozen graph to  tflite format
    - Where we use frozen graph file generated by `run_frozen_pb_convertor`

Note that you can apply these script to your own Tensorflow lite model conversion 
once you have your own graphdef and checkpoint files.


In other ways, you can use `tf.contrib.toco_convert` for direct `.tflife`-conversion from Tensorflow scripts.
- For detail, see [related Tensorflow API document](https://www.tensorflow.org/versions/master/api_docs/python/tf/contrib/lite/toco_convert).


## Feedback 
- Issues: report issues, bugs, and request new features
- Pull request
- Email: jwkang10@gmail.com

## License
- Apach License 2.0


## Authors Information 
- Jaewook Kang Ph.D.
- [Personal website](https://sites.google.com/site/jwkang10/)
- [Facebook](https://www.facebook.com/jwkkang)
- [Linkedin](https://www.linkedin.com/in/jaewook-kang-3a4217b9/)


## Code References
- [Google freeze_graph.py](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/python/tools/freeze_graph.py)
- [Google toco_from_protos.py](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/contrib/lite/toco)
- [Google Tensorflow document](https://www.tensorflow.org/mobile/prepare_models)