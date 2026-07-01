# toyproject_Vision_Hailo-8_on_ExynosAuto
Yolo Vision acceleration using Hailo-8 on ExynosAuto SoC

### 1. HAILO-8  AI Accelerator for VISION 
<img width="2263" height="717" alt="image" src="https://github.com/user-attachments/assets/6e7bf1e4-2050-44ec-9682-a988e9db44e1" />

- [AI M.2 Accelerator: Hailo-8 AI Module | Superior Edge Performance](https://hailo.ai/products/ai-accelerators/hailo-8-m2-ai-acceleration-module/)
- Technical Specifications

| Form Factor              | M.2 Key M                                                                  | Key B+M                              | Key A+E    |
| ------------------------ | -------------------------------------------------------------------------- | ------------------------------------ | ---------- |
| **AI Processor**         | Hailo-8 AI processor with up to 26 TOPS and best-in-class power efficiency |                                      |            |
| **Dimensions**           | 22 x 42 mm with breakable extensions to 22 x 60 and 22 x 80 mm             |                                      | 22 x 30 mm |
| **Interface**            | PCIe Gen-3.0, 4 lanes (up to 32 Gbs)                                       | PCIe Gen-3.0, 2 lanes (up to 16 Gbs) |            |
| **Supported Frameworks** | TensorFLow, TensorFlow Lite, ONNX, Keras, Pytorch                          |                                      |            |
| **Supported OS**         | Linux, Windows                                                             |                                      |            |
| **Certification**        | CE, FCC                                                                    |                                      |            |


### 2. Module on KITT1 Discovery-V9 Board
- M.2 M-KEY, PCIe Gen3 x4 Lane port
- Ubuntu 20.04 with KITT1 SDK v1.2 
- Network enabled with VirtualBox NAT
- Picture
<img width="1413" height="1791" alt="image" src="https://github.com/user-attachments/assets/b198763d-7dff-438f-86e9-4f6cec3f54d4" />


### 3. PCI enumeration
- After boot-up KITT1, please do "lspci" to detect HAILO-8 device.
```
exynosauto@ubuntu:~$ lspci
0000:00:00.0 PCI bridge: Samsung Electronics Co Ltd Device ecec (rev 01)
0000:01:00.0 Co-processor: Device 1e60:2864 (rev 01)
0001:00:00.0 PCI bridge: Samsung Electronics Co Ltd Device eced (rev 01)
0002:00:00.0 PCI bridge: Samsung Electronics Co Ltd Device ecf0 (rev 01)
0002:01:00.0 Network controller: Broadcom Inc. and subsidiaries Device 4415 (rev 0d)

exynosauto@ubuntu:~$ lspci -nn | grep -i "1e60"
0000:01:00.0 Co-processor [0b40]: Device [1e60:2864] (rev 01)
```
- Detail information 
```
exynosauto@ubuntu:~$ sudo lspci -d 1e60:2864 -vvv
[sudo] password for exynosauto: 

0000:01:00.0 Co-processor: Device 1e60:2864 (rev 01)
	Subsystem: Device 1e60:2864
	Control: I/O- Mem- BusMaster- SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx-
	Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-
	Interrupt: pin A routed to IRQ 0
	Region 0: Memory at 20000000 (64-bit, prefetchable) [disabled] [size=16K]
	Region 2: Memory at 20008000 (64-bit, prefetchable) [disabled] [size=4K]
	Region 4: Memory at 20004000 (64-bit, prefetchable) [disabled] [size=16K]
	Capabilities: [80] Express (v2) Endpoint, MSI 00
		DevCap:	MaxPayload 256 bytes, PhantFunc 0, Latency L0s unlimited, L1 unlimited
			ExtTag+ AttnBtn- AttnInd- PwrInd- RBE+ FLReset+ SlotPowerLimit 0.000W
		DevCtl:	CorrErr- NonFatalErr- FatalErr- UnsupReq-
			RlxdOrd+ ExtTag+ PhantFunc- AuxPwr- NoSnoop+ FLReset-
			MaxPayload 128 bytes, MaxReadReq 512 bytes
		DevSta:	CorrErr- NonFatalErr- FatalErr- UnsupReq- AuxPwr- TransPend-
		LnkCap:	Port #0, Speed 8GT/s, Width x4, ASPM L0s L1, Exit Latency L0s <1us, L1 <2us
			ClockPM- Surprise- LLActRep- BwNot- ASPMOptComp+
		LnkCtl:	ASPM Disabled; RCB 64 bytes Disabled- CommClk-
			ExtSynch- ClockPM- AutWidDis- BWInt- AutBWInt-
		LnkSta:	Speed 2.5GT/s (downgraded), Width x2 (downgraded)
			TrErr- Train- SlotClk+ DLActive- BWMgmt- ABWMgmt-
		DevCap2: Completion Timeout: Not Supported, TimeoutDis+, NROPrPrP-, LTR+
			 10BitTagComp-, 10BitTagReq-, OBFF Not Supported, ExtFmt+, EETLPPrefix-
			 EmergencyPowerReduction Not Supported, EmergencyPowerReductionInit-
			 FRS-, TPHComp-, ExtTPHComp-
			 AtomicOpsCap: 32bit- 64bit- 128bitCAS-
		DevCtl2: Completion Timeout: 50us to 50ms, TimeoutDis-, LTR-, OBFF Disabled
			 AtomicOpsCtl: ReqEn-
		LnkCtl2: Target Link Speed: 8GT/s, EnterCompliance- SpeedDis-
			 Transmit Margin: Normal Operating Range, EnterModifiedCompliance- ComplianceSOS-
			 Compliance De-emphasis: -6dB
		LnkSta2: Current De-emphasis Level: -6dB, EqualizationComplete+, EqualizationPhase1-
			 EqualizationPhase2-, EqualizationPhase3-, LinkEqualizationRequest-
	Capabilities: [e0] MSI: Enable- Count=1/1 Maskable- 64bit+
		Address: 0000000000000000  Data: 0000
	Capabilities: [f8] Power Management version 3
		Flags: PMEClk- DSI- D1- D2- AuxCurrent=0mA PME(D0-,D1-,D2-,D3hot+,D3cold-)
		Status: D0 NoSoftRst+ PME-Enable- DSel=0 DScale=1 PME-
	Capabilities: [100 v1] Vendor Specific Information: ID=1556 Rev=1 Len=008 <?>
	Capabilities: [108 v1] Latency Tolerance Reporting
		Max snoop latency: 0ns
		Max no snoop latency: 0ns
	Capabilities: [110 v1] L1 PM Substates
		L1SubCap: PCI-PM_L1.2+ PCI-PM_L1.1+ ASPM_L1.2+ ASPM_L1.1+ L1_PM_Substates+
			  PortCommonModeRestoreTime=10us PortTPowerOnTime=10us
		L1SubCtl1: PCI-PM_L1.2- PCI-PM_L1.1- ASPM_L1.2- ASPM_L1.1-
			   T_CommonMode=0us LTR1.2_Threshold=0ns
		L1SubCtl2: T_PwrOn=10us
	Capabilities: [128 v1] Alternative Routing-ID Interpretation (ARI)
		ARICap:	MFVC- ACS-, Next Function: 0
		ARICtl:	MFVC- ACS-, Function Group: 0
	Capabilities: [200 v2] Advanced Error Reporting
		UESta:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UEMsk:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UESvrt:	DLP+ SDES- TLP- FCP+ CmpltTO- CmpltAbrt- UnxCmplt- RxOF+ MalfTLP+ ECRC- UnsupReq- ACSViol-
		CESta:	RxErr- BadTLP- BadDLLP- Rollover- Timeout- AdvNonFatalErr-
		CEMsk:	RxErr- BadTLP- BadDLLP- Rollover- Timeout- AdvNonFatalErr+
		AERCap:	First Error Pointer: 00, ECRCGenCap+ ECRCGenEn- ECRCChkCap+ ECRCChkEn-
			MultHdrRecCap- MultHdrRecEn- TLPPfxPres- HdrLogCap-
		HeaderLog: 00000000 00000000 00000000 00000000
	Capabilities: [300 v1] Secondary PCI Express
		LnkCtl3: LnkEquIntrruptEn-, PerformEqu-
		LaneErrStat: 0
lspci: Unable to load libkmod resources: error -12

exynosauto@ubuntu:~$ 
```



### 4. Kernel 5.15.74 ready for KITT1 Ubuntu 20.04
Ubuntu 20.04에서 HAIL-8 module의 kernel driver module을 빌드하기 위해서 
현재 Ubuntu 22.04 rootfs과 같이 구동되고 잇는 Linux 5.15.74의 kernel source를 rootfs에 준비해야한다.

- 일단 KITT1 5.15.74 kernel source를 보드의 rootfs안으로 네트워그 enable상태에서 scp로 가져온다.  (/lib/modules/5.15.74/build 가 기본 folder가 그 안으로 kernel source를 가져옴)
```
cd /usr/src
scp -r js0526.park@12.81.221.237:/home1/js0526.park/PRJ/Discovery-V9/10_kernel_bsp/sdk_v1.2/sources/kernel.7z .
tar xf kernel.7z
mv kernel linux-5.15.74
```
- 가져온 KITT1 kernel source를 일단 .config로 전체를 정리하기 위해서 (module 빌드를 위한 header 정리등) 한번 config한후 빌드해보도록 하자.
```
sudo apt install flex bison libssl-dev

sudo rm -rf /lib/modules/5.15.74/build  
sudo ln -s /usr/src/linux-5.15.74 /lib/modules/5.15.74/build   
cd build

cd /lib/modules/5.15.74/build
zcat /proc/config.gz > .config

make olddefconfig 
make prepare
make modules_prepare 
```
- 이제 kernel전체를 빌드를 해야지 Module.symvers 등 아래 HAILO-8의 kernel driver module빌드가 가능하다.
```
make -j$(nproc)
make modules_install
```



### 5. HAILO-8 kernel PCIE driver
- vision용 hailo-8은 아래 공식 driver site에서 hailo8 브랜치에서 받아온다
```
cd ~/50_HAILO-8

git clone -b hailo8 https://github.com/hailo-ai/hailort-drivers.git
```
- 빌드하기전에 firmware를 먼저  download받아서 미리 설치한다.
```
cd hailort-drivers
  
./download_firmware.sh 

sudo mkdir -p /lib/firmware/hailo
sudo cp hailo8_fw.4.23.0.bin  /lib/firmware/hailo/hailo8_fw.bin
sudo chmod 644 /lib/firmware/hailo/hailo8_fw.bin
```
- 이제 kernel driver를 빌드해본다
```
cd linux/pcie

make all  
sudo make install
```
- 빌드된 module을 load해서 device node가 나타나는지 확인한다
```
sudo depmod -a

sudo modprobe hailo_pci
lsmod | grep hailo  
dmesg | grep -i hailo  
ls -al /dev/hailo*

crw------- 1 root root 234, 0 May 19 14:12 /dev/hailo0
```
- 이제 일반 user에서 Hailo-b module을 접근하기 위해서 아래와 같이 udev rule을 업데이트한다
```
sudo cp ./51-hailo-udev.rules /etc/udev/rules.d/  
sudo udevadm control --reload-rules  
sudo udevadm trigger

$ ls -al /dev/hailo0 
crw-rw-rw- 1 root root 234, 0 May 19 14:15 /dev/hailo0
```


### 6. Hailo-RT build
- Userspace package인 Hailo-RT를 deb를 사이트에서 받아서 해도 되지만, 소스를 직접 받아서 빌드해보자
```
cd ~/50_HAILO-8

git clone https://github.com/hailo-ai/hailort.git  
cd hailort
git checkout v4.23.0

sudo apt update  
sudo apt install -y build-essential cmake git libssl-dev pkg-config

cmake -S . -B build -DCMAKE_BUILD_TYPE=Release  
cmake --build build -j$(nproc)

sudo cmake --build build --target install
```
- /usr/local에 설치된다.

- 아래와 같이 빌드가 된 hailortcli 로 기본  연결 test를 한다
```
$ hailortcli --version
HailoRT-CLI version 4.23.0

$ sudo hailortcli scan
Hailo Devices:
[-] Device: 0000:01:00.0


$ sudo hailortcli fw-control identify
Executing on device: 0000:01:00.0
Identifying board
Control Protocol Version: 2
Firmware Version: 4.23.0 (release,app,extended context switch buffer)
Logger Version: 0
Board Name: Hailo-8
Device Architecture: HAILO8
```

- 이제 간단한 model을 다운받자.
```
mkdir -p ~/50_HAILO-8/models  
cd ~/50_HAILO-8/models

wget https://hailo-model-zoo.s3.eu-west-2.amazonaws.com/ModelZoo/Compiled/v2.9.0/yolov8n.hef
```

- 이제 Yolo8n을 간단하게 benchmark test 헤보자 (약 200 fps정도가 나온다)
```
exynosauto@ubuntu:~/50_HAILO-8/models$ hailortcli parse-hef yolov8n.hef
Architecture HEF was compiled for: HAILO8
Network group name: yolov8n, Single Context
    Network name: yolov8n/yolov8n
        VStream infos:
            Input  yolov8n/input_layer1 UINT8, NHWC(640x640x3)
            Output yolov8n/conv41 UINT8, FCR(80x80x64)
            Output yolov8n/conv42 UINT8, FCR(80x80x80)
            Output yolov8n/conv52 UINT8, FCR(40x40x64)
            Output yolov8n/conv53 UINT8, FCR(40x40x80)
            Output yolov8n/conv62 UINT8, NHWC(20x20x64)
            Output yolov8n/conv63 UINT8, FCR(20x20x80)
            
exynosauto@ubuntu:~/50_HAILO-8/models$ sudo hailortcli benchmark yolov8n.hef
Starting Measurements...
Measuring FPS in HW-only mode
Network yolov8n/yolov8n: 100% | 3026 | FPS: 201.64 | ETA: 00:00:00
Measuring FPS (and Power on supported platforms) in streaming mode
Network yolov8n/yolov8n: 100% | 3026 | FPS: 201.64 | ETA: 00:00:00
Measuring HW Latency
Network yolov8n/yolov8n: 100% | 2123 | HW Latency: 6.51 ms | ETA: 00:00:00

=======
Summary
=======
FPS     (hw_only)                 = 201.642
        (streaming)               = 201.642
Latency (hw)                      = 6.50882 ms
exynosauto@ubuntu:~/50_HAILO-8/models$ 
```


### 7. Hailo-RT whl 
- 보드에서 python관련 설정은 아래와 같이 미리 해놓아야한다.
```
mkdir -p ~/.config/pip
vi ~/.config/pip/pip.conf

[global]
trusted-host = pypi.python.org
               pypi.org
               files.pythonhosted.org
               download.pytorch.org
               ftp.daumkakao.com
               github.com
proxy = http://12.26.204.100:8080

sudo apt install python3.8-venv
```

- 이제 HailoRT에서 python example을 수행해보기 위해서 whl을 만들어야 하는데.. 개발자사이트에서 다운받아도 되지만 직접 만들어보자
```
$ cd ~/50_HAILO-8/hailort/hailort/libhailort/bindings/python/platform  
$ python3 -m pip install --upgrade pip setuptools wheel  
$ python3 setup.py bdist_wheel
$ find . -name "*.whl"
./dist/hailort-4.23.0-cp38-cp38-linux_aarch64.whl
```
일단 만들어진것만 확인하고 넘어가자..




### 8. Pyhton - Object detecton Example
- 이제 Example Repo를 받아서 Object Detection example을 python으로 수행해본다
- venv에 아까 생성해놓은 whl을 설치해서 해보자
```
cd ~/50_HAILO-8
git clone https://github.com/hailo-ai/Hailo-Application-Code-Examples.git  
cd Hailo-Application-Code-Examples/runtime/python/object_detection
 
python3 -m venv venv
source venv/bin/activate

pip install --upgrade pip
pip install -r requirements.txt

pip install ~/50_HAILO-8/hailort/hailort/libhailort/bindings/python/platform/dist/hailort-*.whl

python3 -c "import hailo_platform; print('PyHailoRT OK')"
```

- 되긴한데.. 현재 python3.8이라 type관련 오류가 발생한다.
```
python3 object_detection.py -n ~/50_HAILO-8/models/yolov8n.hef -i ~/50_HAILO-8/video.mp4
```

> [!info] NOTICE
> example Python의 type관련 오류는 python3.10이상을 써야하는데 일단 현재 Discovery-V9 Ubuntu 20.04에서는 당장 지원이 되지 않는다. 
> Python 3.10을 별도로 설치하거나, Docker로 Ubuntu 22.04이상을 사용해서 진행이 가능하지만 일단 Python 예제는 시간관계상 다음이 진행하고. 현상태에서 HOLD하기로 한다.



### 9. C++  - Object detecton Example
- 사전에 같이 제공되는 C++ example code를 돌려보자
- 필요한 package는사전에 설치해야한다.
```
sudo apt update  
sudo apt install -y libopencv-dev python3-opencv pkg-config jq

sudo apt install -y libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev gstreamer1.0-tools gstreamer1.0-plugins-base \
gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly

pkg-config --modversion opencv4
4.2.0

sudo apt install -y ocl-icd-opencl-dev opencl-headers
```
- 이제 C++ Object Detection예제를 빌드해보자
```
cd ~/50_HAILO-8
git clone https://github.com/hailo-ai/Hailo-Application-Code-Examples.git  
cd ~/50_HAILO-8/Hailo-Application-Code-Examples/runtime/cpp/object_detection/

mkdir -p build  
cd build  

//opencl 때문에.. :   /usr/bin/ld: /usr/lib/aarch64-linux-gnu/libavutil.so: undefined reference to `clReleaseMemObject@OPENCL_1.0'

cmake .. \
-DCMAKE_PREFIX_PATH=/usr/local \
-DCMAKE_EXE_LINKER_FLAGS="-Wl,--allow-shlib-undefined"

make -j$(nproc)
```
- 빌드한걸 아래와 같이 수행해볼수 있다.
- 일단 정확한 test를 위해서 Discovery-V9보드를 재부팅하고 HAILO-9 KMD도 다시 loading해서 test한다.
```
sudo date -s "$(curl -sI http://www.example.com | grep ^Date: | cut -d' ' -f2- | xargs -I{} date -d "{}" +"%Y-%m-%d %H:%M:%S")"

// module 연결이 정상인지
sudo modprobe -r hailo_pci  
sudo modprobe hailo_pci
hailortcli scan  
hailortcli fw-control identify

$ ./object_detection --net yolov8n --arch hailo8 --input ~/50_HAILO-8/video.mp4

./object_detection: /lib/aarch64-linux-gnu/libmali.so.0: no version information available (required by /lib/aarch64-linux-gnu/libavutil.so.56)
./object_detection: /lib/aarch64-linux-gnu/libmali.so.0: no version information available (required by /lib/aarch64-linux-gnu/libavutil.so.56)
You passed a model name: 'yolov8n'. Searching for this model in the supported networks... please wait.
Downloading model name yolov8n, please wait...
Download complete: "/home/exynosauto/50_HAILO-8/Hailo-Application-Code-Examples/runtime/cpp/object_detection/build/yolov8n.hef"
-I- Detected video file input: /home/exynosauto/50_HAILO-8/video.mp4
-I-----------------------------------------------
-I-  Network Name
-I-----------------------------------------------
-I   yolov8n.hef
-I-----------------------------------------------
-I-  Input: yolov8n/input_layer1, Shape: (640, 640, 3)
-I-----------------------------------------------
-I-  Output: yolov8n/yolov8_nms_postprocess, Shape: (80, 100, 8000)
-I-----------------------------------------------

Progress: [==================================================] 100% (616/616)
-I-----------------------------------------------
-I- Inference & Postprocess
-I- Average FPS:  29.95
-I- Total time:   20.5676 sec
-I- Latency:      33.389 ms
-I-----------------------------------------------

-I- Application finished successfully
-I- Total application run time: 29.6105 sec
```
- 약 30fps가 나오고 Ubuntu에 입력 video에 대한 결과가 나온다 
- 현재 test board가 power를 측정할수가 없지만, module에 열이 전혀 손으로 느껴지지 않는것으로 보아 매우 저전력인듯 하다.


<img width="1897" height="1088" alt="image" src="https://github.com/user-attachments/assets/980140ad-aee4-4508-b64b-c5cfa7736250" />



