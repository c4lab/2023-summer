# aml-wsi
## PLAN
1. select a whole slide image
2. select region-of-interest (ROI)s from it
3. select images of a single cell from ROIs (called as "tiles")
4. throw tiles into machine learning trying to predict if this WSI have mutated cells or not

## 2023-7-27
1.把上禮拜大家遇到的沒有./model/BestModel.pt的問題解決
2.解決直接用.yml檔案建環境會遇到的問題 => 直接開新的環境, 裝numpy, torch, xlwd, xlrd就可以跑
3.解決torch.load會不小心用到cuda但機器上沒有cuda的問題
>RuntimeError: Attempting to deserialize object on a CUDA device but torch.cuda.is_available() is False. If you are running on a CPU-only machine, please use torch.load with map_location=torch.device(‘cpu’) to map your storages to the CPU.

可以試試在『所有』torch.load(...)加上keyword argument: map_location="cpu" 叫torch使用cpu，別用gpu
```
best_model = torch.load(args.output_dir + f'/BestModel_{i + 1}.pt', map_location="cpu") 
```
待辦事項:
1.whole slide image (e.g. "A314") -> HCT_region_select/main.py -> 輸出一大堆region of interest images（or NOT ROI），並將其絕對路徑存成一個excel檔（已經區分成 ROI vs non-ROI）
2.承接第一步, 用crop_cell函數（參考學長github repo: AML/HCT_cell_detection
/cell_detection_yolov4.py）將ROI images中的每顆細胞照片裁切出來