# nerf_tensorf

### 项目文件结构
TensoRF/
├── colmap/
│ ├── sparse/0/
│ │ ├── cameras.bin
│ │ ├── images.bin
│ │ ├── points3D.bin
│ │ └── project.ini
│ ├── sparse-txt/
│ │ ├── cameras.txt
│ │ ├── images.txt
│ │ └── points3D.txt
│ └── database.db
├── configs/
│ ├── flower.txt
│ ├── lego.txt
│ ├── truck.txt
│ ├── wineholder.txt
│ └── your_own_data.txt
├── data/
│ └── my_object/ 
│ ├── images/ # 多视角原始图像
│ ├── data_process.py 
│ ├── json_process.py 
│ ├── split_summary.json
│ ├── transforms_test.json
│ ├── transforms_train.json
│ ├── transforms_val.json
│ └── transforms.json
├── dataLoader/
│ ├── colmap2nerf.py # COLMAP转NeRF格式脚本
│ ├── your_own_data.py 
└── train.py

###环境要求
conda create -n TensoRF python=3.8
pip install torch torchvision
pip install tqdm scikit-image opencv-python configargparse lpips imageio-ffmpeg kornia lpips tensorboard



