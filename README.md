![DroidBot UTG](droidbot/resources/dummy_documents/droidbot_utg.png)

# DroidBot


      env
         conda create -n droidbot python=3.10.8 
         
         if silicon mac:
            conda install -c apple tensorflow-deps  # v2.10.0 in mac studio, v2.9.0 in astroboi_m2
            python -m pip install tensorflow-macos  # v2.13.0 in astroboi_m2
            python -m pip install tensorflow-metal  # v1.0.1 in astroboi_m2
            python -m pip install scikit-learn  # v1.3.0 in astroboi_m2

         elif windows:
            conda install -c conda-forge tensorflow  # v2.10.0 in mac studio
            conda install -c anaconda scikit-learn  

         pip install opencv-python==4.5.4.60  # cv2는 반드시 pip 설치
         conda install -c pytorch pytorch=2.0.1  # pytorch, pytorchvision 부터 깔기
         conda install -c pytorch torchvision
         ~~conda install -c anaconda networkx=2.8.4~~  # torchvision 깔 때 같이 깔림
         pip install androguard==3.4.0a1
         pip install Frida-tools==12.1.2
         conda install -c conda-forge gym=0.21.0 # 강화학습 개발 위한 패키지 gym 
         conda install -c conda-forge imageio=2.31.1 # 영상, 이미지 관련 패키지  
         conda install -c anaconda chardet  # 4.0.0


## New!

:fire: We recently integrated ChatGPT into DroidBot to support automating any app with a simple text prompt. [Take a look!](https://github.com/GAIR-team/DroidBot-GPT)


## About
DroidBot is a lightweight test input generator for Android.
It can send random or scripted input events to an Android app, achieve higher test coverage more quickly, and generate a UI transition graph (UTG) after testing.

A sample UTG is shown [here](http://honeynet.github.io/droidbot/report_com.yelp.android/).

DroidBot has the following advantages as compared with other input generators:

1. It does not require system modification or app instrumentation;
2. Events are based on a GUI model (instead of random);
3. It is programmable (can customize input for certain UI);
4. It can produce UI structures and method traces for analysis.

**Reference**

[Li, Yuanchun, et al. "DroidBot: a lightweight UI-guided test input generator for Android." In Proceedings of the 39th International Conference on Software Engineering Companion (ICSE-C '17). Buenos Aires, Argentina, 2017.](http://dl.acm.org/citation.cfm?id=3098352)

## Prerequisite

1. `Python` (both 2 and 3 are supported)
2. `Java`
3. `Android SDK`
4. Add `platform_tools` directory in Android SDK to `PATH`
5. (Optional) `OpenCV-Python` if you want to run DroidBot in cv mode.

## How to install

Clone this repo and install with `pip`:

```shell
git clone https://github.com/honeynet/droidbot.git
cd droidbot/
pip install -e .
```

If successfully installed, you should be able to execute `droidbot -h`.

## How to use

1. Make sure you have:

    + `.apk` file path of the app you want to analyze.
    + A device or an emulator connected to your host machine via `adb`.

2. Start DroidBot:

    ```
    droidbot -a <path_to_apk> -o output_dir
    ```
    That's it! You will find much useful information, including the UTG, generated in the output dir.

    + If you are using multiple devices, you may need to use `-d <device_serial>` to specify the target device. The easiest way to determine a device's serial number is calling `adb devices`.
    + On some devices, you may need to manually turn on accessibility service for DroidBot (required by DroidBot to get current view hierarchy).
    + If you want to test a large scale of apps, you may want to add `-keep_env` option to avoid re-installing the test environment every time.
    + You can also use a json-format script to customize input for certain states. Here are some [script samples](script_samples/). Simply use `-script <path_to_script.json>` to use DroidBot with a script.
    + If your apps do not support getting views through Accessibility (e.g., most games based on Cocos2d, Unity3d), you may find `-cv` option helpful.
    + You can use `-humanoid` option to let DroidBot communicate with [Humanoid](https://github.com/yzygitzh/Humanoid) in order to generate human-like test inputs.
    + You may find other useful features in `droidbot -h`.

## Evaluation

We have conducted several experiments to evaluate DroidBot by testing apps with DroidBot and Monkey.
The results can be found at [DroidBot Posts](http://honeynet.github.io/droidbot/).
A sample evaluation report can be found [here](http://honeynet.github.io/droidbot/2015/07/30/Evaluation_Report_2015-07-30_1501.html).

## Acknowledgement

1. [AndroidViewClient](https://github.com/dtmilano/AndroidViewClient)
2. [Androguard](http://code.google.com/p/androguard/)
3. [The Honeynet project](https://www.honeynet.org/)
4. [Google Summer of Code](https://summerofcode.withgoogle.com/)

## Useful links

- [DroidBot Blog Posts](http://honeynet.github.io/droidbot/)
- [droidbotApp Source Code](https://github.com/ylimit/droidbotApp)
- [How to contact the author](http://ylimit.github.io)
