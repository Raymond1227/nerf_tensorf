# nerf_tensorf  
项目结构
```
TensoRF/
├── colmap/
│   ├── sparse/0/
│   │   ├── cameras.bin
│   │   ├── images.bin
│   │   ├── points3D.bin
│   │   └── project.ini
│   ├── sparse-txt/
│   │   ├── cameras.txt
│   │   ├── images.txt
│   │   └── points3D.txt
│   └── database.db
├── configs/
│   └── your_own_data.txt
├── data/
│   └── my_object/
│       ├── images/         # 多视角原始图像
│       ├── data_process.py
│       ├── json_process.py
│       ├── split_summary.json
│       ├── transforms_test.json
│       ├── transforms_train.json
│       ├── transforms_val.json
│       └── transforms.json
├── dataLoader/
│   ├── colmap2nerf.py      # COLMAP转NeRF格式脚本
│   └── your_own_data.py
└── train.py
```

# 环境要求  
conda create -n TensoRF python=3.8  
pip install torch torchvision  
pip install tqdm scikit-image opencv-python configargparse lpips imageio-ffmpeg kornia lpips tensorboard  
conda install -c conda-forge colmap  
pip install protobuf==3.20.0  


# colmap数据处理  
cd TensoRF  

colmap feature_extractor \
   --database_path ./colmap/database.db \
   --image_path ./images

colmap exhaustive_matcher \
   --database_path ./colmap/database.db

mkdir ./colmap/sparse

colmap mapper \
   --database_path ./colmap/database.db \
   --image_path ./images \
   --output_path ./colmap/sparse

mkdir -p ./colmap/sparse-txt  

colmap model_converter \
   --input_path ./colmap/sparse/0 \
   --output_path ./colmap/sparse-txt \
   --output_type TXT

## 使用 colmap2nerf.py 转换为 transforms.json  
python dataLoader/colmap2nerf.py   
   --text ./colmap/sparse-txt   
   --images ./images   
   --out ./data/my_object/transforms.json

## transforms.json分为train test val  
python data_process.py  

# 训练  
python train.py --config configs/your_own_data.txt --datadir ./data/my_object  
tensorboard --logdir /log/tensorf_shoes_VM --port 6001






