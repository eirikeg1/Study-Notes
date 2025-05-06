


# All frames
---
![[Pasted image 20250502162157.png]]
![[Pasted image 20250505015520.png]]
(dribling-detection) ➜  dribbling-detection-pipeline git:(main) ✗ python src/evalutation.py
Evaluated 57 clips

![[Pasted image 20250503143001.png]]

![[Pasted image 20250506010904.png]] ([ChatGPT](https://chatgpt.com/c/68194447-8eac-8006-a16f-1b8f6472bf45) Analysis)


## Not interpolated
mAP@[0.5, 0.55, 0.6, 0.65, 0.7, 0.75, 0.8, 0.85, 0.9, 0.95] (image): 0.3094   mIoU (image): 0.4828
mAP@[0.5, 0.55, 0.6, 0.65, 0.7, 0.75, 0.8, 0.85, 0.9, 0.95] (pitch):  0.0033   mIoU (pitch):  0.1656
![[Pasted image 20250504201525.png]]

![[Pasted image 20250502232825.png]]

## Interpolated
![[Pasted image 20250504195949.png]]

![[Pasted image 20250502234927.png]]

ball 15 and player 75 on the top and b15 p35 below:
![[Pasted image 20250503153816.png]]
# Interpolated f-2
---
![[Pasted image 20250502204802.png]]mAP@[0.5, 0.55, 0.6, 0.65, 0.7, 0.75, 0.8, 0.85, 0.9, 0.95] (image): 0.6924   mIoU (image): 0.8201
mAP@[0.5, 0.55, 0.6, 0.65, 0.7, 0.75, 0.8, 0.85, 0.9, 0.95] (pitch):  0.0044   mIoU (pitch):  0.1717

![[Pasted image 20250504200432.png]]
![[Pasted image 20250502232838.png]]

# Interpolated f=3
---
![[Pasted image 20250503012929.png]]
![[Pasted image 20250504195916.png]]


![[Pasted image 20250504011307.png]]