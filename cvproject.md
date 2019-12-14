# 记录在github上运行的各类CV项目的坑

### SiamMask运行日志
在siammask_sharp目录下输入下面语句
```
export PYTHONPATH =$PYTHONPATH:/home/syk/SiamMask
```
在测试SiamMask的tracker时候，下载王强给出了三个训练模型即可，当然你可以根据你的数据集需要来下载模型
需要说明的vot2016运行的参数会有问题，建议在vot2018上运行，也就是在siammask_sharp下执行
```
bash test_mask_refine.sh config_vot.json SiamMask_VOT.pth VOT2018 0
python ../../tools/eval.py --dataset VOT2018 --tracker_prefix C --result_dir ./test/VOT2018
````
如果你在执行上面第一句时无法成功下载解压vot，你可以将vot数据集拷贝到data目录下。
需注意两点  
* VOT2018这个文件名需要根据代码中的实际情况来做大小写  
* 同时数据集里面需要有list.txt这个清单文件

### atom和dimp的pytracking运行
你可以在[here](https://github.com/visionml/pytracking)找到代码并拷贝下来
建立虚拟环境
```
 conda creative -n pytracking python=3.6
```
然后需要下载马丁提供的四个模型将模型放在pytracking/pytracking/networks目录下
分别是这四个dimp50.pth,dimp18.pth,atom_default.pth,resnet18_vggmconv1.pth可以根据自己的实际需求放,然后测试运行
```
conda activate pytracking
cd pytracking
python run_webcam.py dimp dimp50
如果你的电脑没有摄像头，只要弹出窗口既代表成功了
```
测试部分运行参数在run_tracker.py中。根据参数执行：
```
python run_tracker.py atom default --dataset otb --sequence Soccer --debug 8 --threads 0
```
这里简单说明一下，运行之前需要确认自己的cuda和cudnn安装完毕。这里的sequence是运行那个序列，debug表示运行级别０－９，表示提显示多少信息。threads表示用几个线程去做
